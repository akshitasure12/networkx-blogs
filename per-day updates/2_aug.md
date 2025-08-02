## 2nd Aug
**Total Combined hours : 4 hours**

### Comparing betweenness and harmonic centrality
**Duration: [2 hours]** </br>
**Associated PR: [PR#124](https://github.com/networkx/nx-parallel/pull/124)**

1. Why betweeness centrality shows speedups and harmonic centrality doesnt?
    - Both of them pass huge graphs, so that could not be the bottleneck
    - Both compute shortest paths
    - I think the main difference would be the computation performed after the shortest path calculation.
    - Tried a way of using all pairs shortest paths instead.
    - added a short circuit.

End Result: Nothing resulted in a speedup, so I am inclined to add a should_run parameter.

### Additional work done:
**Duration: [2 hours]** </br>
1. Explored trying to implement parallel `number_of_cliques`.
    - But that would imply only parallelising a section of the code (the if section) and not the rest.
    - It would mostly not give any speedups because it would only parallelise the `sum` aspect of it.
2. Most of the PRs were not up to date with the codebase, so I resolved their merge conflicts and brought them up to date with the main codebase.
3. Go through all the review comments and fix the loose ends.
