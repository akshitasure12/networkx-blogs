## 19th Aug
**Total Combined hours : 4 hours**

### Updated open PRs
**Duration: [2 hours]** </br>

1. Rebased PRs after recent merges into main.
2. Observed failing changes in `test_should_run.py`
    - default `n_jobs` is `None` but with the PR, make `n_jobs=-1` merged, it fails CI related tests.
3. Checked for areas of improvement.

### Raised a PR to accomodate failing changes
**Duration: [2 hours]** </br>
**Associated PR: https://github.com/networkx/nx-parallel/pull/138**

1. Update `README.md` with the latest algorithms.
2. Moved merged algorithms PR heatmaps to their respective directories.
3. Re-ran all of link prediction algorithms with the new timing script.
4. Fixed failing test using a networkx config context manager.
5. Modified timing_script to include community algorithms.


