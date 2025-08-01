## 1st Aug
**Total Combined hours : 7 hours**

### Review Comments 
**Duration: [2 hours]** </br>

1. [adding `should_run` parameter](https://github.com/networkx/nx-parallel/pull/123)
    - Adding a default `should_run` to use more than 1 job.
    - added should run for more algorithms.
2. asv `setup` function PR
    - Verified benchmarks to see if I got any error, but I didn't get any.
    - Entering all the changes made to benchmarks in `README.md` in the asv benchmarks PR.


### Added implementation of `average_neighbor_degree`
**Duration: [3 hours]** </br>
**Associated PR:** [PR#132](https://github.com/networkx/nx-parallel/pull/132)

1. Added the revised implementation of algorithm.
2. Handled a NodeView error encountered in teh process (the nodes=node condition which took some time to debug).
3. Added benchmarks using the setup function approach.
    - tried it by setting different `n_jobs` values but no speedups encountered, performance only became worse with increasing workers.
4. tested it against the timing script which didnt give speedsups.
    - reasons likely : low computation in each chunk and overhead.
    - tried with a maximum chunk size as well.


### Spent time reading and experimenting with a few old PRs:
**Duration: [2 hours]** </br>

1. [PR#74](https://github.com/networkx/nx-parallel/pull/74): 
    - Re-open the respective PR and add `should_run` to the respective algorithms.
2. [PR#33](https://github.com/networkx/nx-parallel/pull/33)
3. [PR#49](https://github.com/networkx/nx-parallel/pull/49)

