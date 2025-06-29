# Blog2
## Week 3-4 (16th June to 29th June, 2025)

## Abstract

During weeks 3–4 of my coding phase, I focused on several key enhancements. The most significant was the addition of the `should_run` parameter allowing algorithms to decide at runtime whether the parallel backend is beneficial— helping avoid unnecessary overhead for fast, lightweight functions like `number_of_isolates`. I also contributed to improving the documentation by setting `n_jobs=-1` and switching the default configuration from Joblib configs to Networkx configs. I also understood how context managers work and how they can eliminate test order dependency. Lastly, I worked on adding a NumPy-based implementation of `is_reachable()` with a pure-Python fallback, enabling speed improvements while maintaining compatibility for users without NumPy installed.

## Details

### 1. Adding `should_run` parameter 

For algorithms whose NetworkX implementation is already very fast (such as `number_of_isolates`), it can be inefficient to invoke the parallel backend due to the overhead of graph conversion and parallel setup. To address this, we need to implement a `should_run` mechanism that allows each parallel algorithm to dynamically decide at runtime whether it should run the backend implementation. This mechanism is triggered only when the input graph is a standard NetworkX graph and the backend system is attempting to decide whether it should convert the graph to a `ParallelGraph` and dispatch to a backend. It is not triggered when a backend is explicitly provided in the function call, or when the input is already a backend-specific graph (like `ParallelGraph`).

To support this, I added a `should_run` method to the `BackendInterface` class. When a parallel implementation is available for a given algorithm, this method checks whether a custom `should_run` function has been defined for that specific algorithm. If it has, the dispatcher invokes that function to determine whether it is beneficial to run the backend. If no such function is defined, it falls back to a default `True` value, meaning the backend is allowed to run.

Each custom `should_run` function is registered to its algorithm via the `_should_run` decorator, defined inside the `_configure_if_nx_active()` wrapper. For instance, in the `number_of_isolates` implementation, I defined a custom function decorated by `number_of_isolates._should_run` that returns the following string explanation: "Fast algorithm; not worth converting" when it is executed. The return type of this function is either `True` i.e runs the backend, `False` to not run the backend or False with an explanation (a string). This indicates to the dispatcher that the overhead of parallel execution outweighs any benefit for this specific case, and it skips the backend accordingly. 

Here's a logger example where the custom `should_run` function skips the parallel version for `number_of_isolates`: 

``` console
Call to 'number_of_isolates' has inputs from {'networkx'} backends, and will try to use backends in the following order: ['parallel', 'networkx']
Backend 'parallel' shouldn't run `number_of_isolates` with arguments: (G=<networkx.classes.graph.Graph object at 0x1055fb6e0>), because: Fast algorithm; not worth converting
Trying next backend: 'networkx'
Call to 'isolates' has inputs from {'networkx'} backends, and will try to use backends in the following order: ['parallel', 'networkx']
Backend 'parallel' does not implement 'isolates'
Trying next backend: 'networkx'
5
```
Although I realised and utilised the benefits of logging a little late, it was beneficial to understand the flow. After a review of the implementation, I plan to extend the `should_run` logic to additional algorithms by identifying common patterns based on graph size or structure. For example, backends can skip execution for small graphs:
```python
@sample_algo._should_run
def _(G):
    # here, 10 is a custom threshold
    return G.number_of_nodes() > 10  
```

References used for the implementation:
- [`nx-cugraph` implemntation of `should_run`](https://github.com/rapidsai/cugraph/pull/4348)
- [PR#7257](https://github.com/networkx/networkx/pull/7257)
- [#PR#77](https://github.com/networkx/nx-parallel/issues/77)
- [NetworkX Backend docs](https://networkx.org/documentation/stable/reference/backends.html)


### 2. Make default `n_jobs=-1` in nx-parallel

During my contribution period, I was exploring how decorators work within the nx-parallel backend and noticed that parallelism was not enabled by default. This was surprising as the purpose of using nx-parallel was to take advantage of parallel computation. However, unless the user explicitly set the configuration, all algorithms would execute sequentially.
The users would have to do something like this to enable parallelism:

```python
import joblib

joblib.parallel_config(n_jobs=-1)
```

NetworkX supports two ways of configuring parallelism i.e `joblib.parallel_config` (external) and `nx.config.backends.parallel` (internal to NetworkX). To learn about these configurations, refer to [joblib documentation](https://joblib.readthedocs.io/en/latest/parallel.html) and [NetworkX Backend documentation](https://networkx.org/documentation/latest/reference/backends.html). 

By default, the system relied on joblib, which meant the user had to know and configure `joblib` separately. To simplify this process, we set `n_jobs=-1` (i.e., use all available cores) inside the NetworkX configuration system, and enabled the active flag to `True` by default. 
This change ensures that:
1. Users would get parallelism without delving into the configs part.
2. The default behavior would be consistent with the intent of nx-parallel.

The goal of this PR is to update the documentation reflecting these changes. (ref. [PR#122](https://github.com/networkx/nx-parallel/pull/122)). 


### 3. Utilising context managers for testing

This change was inspired by the discussion in [PR#113](https://github.com/networkx/nx-parallel/pull/113), which highlighted issues with test order dependency. Previously, we used `pytest.mark.order` to force certain tests (that modify global state) to run in a specific sequence in order to not cause unexpected failures. Based on Dan's suggestion, I explored the use of context managers to temporarily modify the tests and reset their configurations afterwards. This approach would make the tests to be more independent of each other.

Although this wasn’t a large code contribution, it was a valuable learning for me considering I hadn't explored the working of context managers before. A youtube video I came across explained this concept really well - https://youtu.be/iba-I4CrmyA?si=e04n48zyrTe1ztHT.

The improvement has been merged in [PR #120](https://github.com/networkx/nx-parallel/pull/120).


### 4. Implementing a fallback for `is_reachable()` in NetworkX
While working on a NumPy-based implementation of `is_reachable()` in NetworkX, I encountered failing CI tests with the error `ModuleNotFoundError: No module named 'numpy'`. This was unexpected, as NumPy was correctly imported in the function. The reason for this failure was that NetworkX also works in environments that don't have numpy installed. As a result of which, unconditionally depending on NumPy would break in these setups, causing the CI failures.

To fix this in the test suite, I was introduced to `np = pytest.importorskip("numpy")` which would import and return the requested module if the module was installed or skip the unit tests otherwise (ref. [doc](https://docs.pytest.org/en/stable/reference/reference.html#pytest.importorskip)). This addressed the failing tests - but it raised a more fundamental issue: how can users without NumPy run `is_reachable()` at all?

To ensure this backward compatibility, a fallback mechanism was to be implemented. If NumPy is available, the optimized NumPy-based version is used. Otherwise, the function falls back to a pure-Python implementation. This approach used [PR#7716](https://github.com/networkx/networkx/issues/7716) and [PR#7718](https://github.com/networkx/networkx/pull/7718) as reference. The general pattern would be:
```python
try:
    import numpy as np
    return _is_reachable_numpy(G, s, t)
except ImportError:
    return _is_reachable_python(G, s, t)
```
This would ensure that users with numpy would benefit from the significant speed-ups in the matrix based implementation and those without numpy, can still use `is_reachable()` with a standard Python implementation. Below is a heatmap demonstrating the observed speedup from switching to the NumPy-based implementation:

![isreachable](../assets/static/numpy_is_reachable.png)
