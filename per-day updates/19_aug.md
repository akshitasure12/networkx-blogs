## 19th Aug
**Total Combined hours : 4 hours**

### Updated open PRs
**Duration: [1.5 hours]** </br>

1. Based on the PRs merged yesterday, I updated the other PR branches.
2. Added `should_run` in necessary algorithms.
3. Bought benchmarks up to date after rebase.

### Added algos in `centrality/reaching.py`
**Duration: [2.5 hours]** </br>
**Associated PR: [PR#123](https://github.com/networkx/nx-parallel/pull/44)**

1. Checked previous implementation of these algorithms.
2. Read the respective algorithm documentation in NetworkX-- understanding what they implement.
3. Read previous implemented code, commits etc. Resolved merge conflicts in the process of rebase.
4. Check whether to add chunks or not?
    - run timing script for both cases
5. Failing CI tests for networkx backend with single node graphs.
6. Failing CI tests for nx-parallel backend - `local_reaching_centrality() missing 1 required positional argument: 'v'`


