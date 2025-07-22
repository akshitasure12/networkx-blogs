## 22nd July
**Total Combined hours : 6 hours**

### Average Degree Neighbor
**Duration: [2 hour]** </br>

1. Began by reading [average neighbor degree](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.assortativity.average_neighbor_degree.html).
2. Added the chunks parameter and the parallel set up for the function.
3. One of the simpler implementations to enforce parallelism I believe, but it requires validation from timing script and benchmarks :)

End Result: I worked out the implementation, need to add benchmarks.

### Clustering algorithm
**Duration: [2 hours]**

1. Began by reading [clustering](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.cluster.clustering.html#networkx.algorithms.cluster.clustering)
2. Initially, I was confused as to how I can parallelise this because it used several helper functions, but then eventually I reached a conclusion that depending on the use case, I would allocate the helper func to `currFunc` -- so I won't have to duplicate the code.
3. The overhead of parallel would dominate for graphs since the computation is purely mathematical.

End Result: I worked out the implementation, need to add benchmarks.

### Adding seperate benchmarks for `is_reachable()`
**Duration: [2 hours]**
**Associated Issue: [Issue#8155](https://github.com/networkx/networkx/issues/8155)

1. breakdown of the 2 benchmarks-
    - source and target from the same strongly connected component, so func should short-circuit early when the target is found.
    - source and target are from different SCCs, he implementation must fully explore the reachable region which gives us the full implementation time.
2. approach followed:
    - Compute SCCs of the test graph (random tournaments).
    - for reachable benchmark: pick two distinct nodes from the same SCC.
    - for unreachable benchmark: pick two nodes from different SCCs.
    - if required, we could remove an edge to break reachability for a pair, ensuring a guaranteed unreachable case in fully connected graphs.
    - this would show us the benefit of short-circuit
3. edge cases:
    - sccs with only one node(not possible in tournaments)

End result: Will raise a PR soon.

