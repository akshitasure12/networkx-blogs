## 6th Aug
**Total Combined hours : 4.5 hours**

### 1. Add parallel `v_structures` and `colliders`
**Duration: [2.5 hours]** </br>
**Associated PR: [PR#134](https://github.com/networkx/nx-parallel/pull/134)**

1. Re-ran all the tests from yesterday, to verify and validate previous performance.
2. Added up final touches (reverting previously made changes to timing script etc).
3. Added heatmaps, fixed the docstrings.
4. Switched the implementation to lazy computing.
5. Ran the benchmarks to see if anything suspicious.
6. Raised a PR and documented the findings and work.

End Result: Raised [PR#134](https://github.com/networkx/nx-parallel/pull/134/)


### 2. Add `average_clustering` algorithm
**Duration: [2 hours]** </br>
**Associated PR: [PR#130](https://github.com/networkx/nx-parallel/pull/130)**

1. Added `average_clustering` to use `nxp.clustering`.
2. Ran into a few rebase errors while took some time to debug.
3. Tried running the benchmark script but the problem of taking up too much time for timing clustering algorithm persisted- heatmap wsn't obtained
    - I ran it for 45 mins but it was still stuck up at 800 nodes with edge_prob = 1
4. Added asv benchmarks.