# Blog3
## Week 5-6 (30th June to 13th July, 2025)

This week was more of a reflection and refinement phase, where I handled detailed review comments and ensured my open pull requests were in good shape for merging.

## Previously Raised Pull requests

1. Simpler Python version for `is_reachable()`
   
   In my last blog post, I had discussed adding separate implementations for the NumPy version and the pure Python version of `is_reachable()`. This week, we explored how to simplify the Python implementation without introducing extra dependencies like `is_path` or even numpy. Instead of iterating through the entire graph again to find two-hop neighbors, we revised the function to use a more direct check using the sucessors of the source node and predeccessors of the target.
    ```python
    return {
        x for x in G if x == v or x in G[v] or any(z in G[v] for z in G.pred[x])
    }
    ```
    This change led to a noticeable reduction in runtime for the sequential (pure Python) version. However, the NumPy implementation still remains faster overall. The results from the timing script below illustrate this difference clearly:
    ```
    Number of nodes: 200
    T1: 0.01871013641357422
    T2: 0.03364920616149902
    Finished <function is_reachable at 0x101504ae0>

    Number of nodes: 400
    T1: 0.07384085655212402
    T2: 0.1333141326904297
    Finished <function is_reachable at 0x101504ae0>

    Number of nodes: 800
    T1: 0.29588794708251953
    T2: 0.5328099727630615
    Finished <function is_reachable at 0x101504ae0>

    Number of nodes: 1600
    T1: 1.215939998626709
    T2: 2.3156769275665283
    Finished <function is_reachable at 0x101504ae0>

    Number of nodes: 3200
    T1: 4.9940502643585205
    T2: 9.749640941619873
    Finished <function is_reachable at 0x101504ae0>
    is_reachable
    ```
    _Here, T1 = NumPy implementation, T2 = pure Python implementation_ </br>

    These tests were run on tournament graphs (directed graphs where each pair of nodes has exactly one directed edge). In such graphs, each node has about `n/2` outgoing edges and `n/2` incoming edges. So when computing two-hop neighborhoods: 

    1. The Python version iterates over about `n/2` predecessors for each candidate node.

    2. The NumPy version, on the other hand, performs `n` direct adjacency matrix lookups.

    For Numpy Implementation to still be faster would mean that numpy lookups are faster than python look ups.

    Overall, these benchmarks show that while the Python implementation is way faster than it was, the NumPy-based approach remains more efficient for larger node counts. 

2. Investigated the use of a global seed set in `improve_timing`

    Initially, I was using `random.seed(42)` globally to set the seed once for the entire script. This worked for generating edge weights, but it didn’t control other random operations — for example, selecting random neighbors.

    Now, I set `seed = random.Random(42)` at the start of the script and pass this `seed` instance when creating graphs. This ensures the entire process is reproducible and produces consistent results for testing. I also used the same `seed` instance to pick random neighbors for bipartite graphs, following suggestions from mentors. This way, we can control all random choices.

    While testing, I also noticed a possible index out-of-bounds issue. To prevent this, I now use the `seed` to pick valid random source and target nodes:
    ```py
    parallelTime = measure_time(H, 1, num)
    ```
    became:
    ```py
    source, target = seed.sample(range(num), 2)
    parallelTime = measure_time(H, source, target)
    ```

These were the major improvements and insights I focused on this week.

### Plan for the upcoming week:

1. I’ve been reading through resources on writing clean, clear documentation as per the recommendations suggested, i.e [Real Python’s guide](https://realpython.com/documenting-python-code/) and [PEP 20 - The Zen of Python](https://peps.python.org/pep-0020/). Using these as a reference, I’m currently refining [PR#122](https://github.com/networkx/nx-parallel/pull/122) to align with best practices.
2. Get a few of the ongoing pull requests merged.
3. Work on new parallel implementations for:
    - `clustering`
    - `average_clustering`
    - `_apply_prediction`
