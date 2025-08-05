## 4th Aug
**Total Combined hours : 3 hours**

### 1. Working on the Closeness centrality PR
**Duration: [2 hours]** </br>
**Associated PR: [PR#72](https://github.com/networkx/nx-parallel/pull/72)**

1. Improved with a few corrections in closeness_centrality (eg: using int instead of float).
2. No speedup obtained as such:
    - Tried timing script with setting a `max_chunk_size`
3. Tried to add `timeit.timeit()` to measure intermediate time but I wasn't successful in finding any diff.
4. Couldn't really capture why the speedups did not reflect
    - I believe it's due to the nature of the algorithm (light weight)


### 2. Move `assign_algorithms` outside `BackendInterface`
**Duration: [1 hour]** </br>
**Associated PR: [PR#133](https://github.com/networkx/nx-parallel/pull/133)**

1. I tried to see how to implement this within the BackendInterface class.
    - This method did not assign properties to the class itself because I could not access the algorithms as BackendInterface attributes.
    - Explored: https://www.geeksforgeeks.org/python/python-locals-function/
2. Adding this just outside the function definition seemed like a better idea instead of using `locals()`.

End Result: Raised [PR#133](https://github.com/networkx/nx-parallel/pull/133)