## 13th Aug
**Total Combined hours : 4.45 hours**

### improve timing
**Duration: [45 mins]** </br>
**Associated issue: [PR#114](https://github.com/networkx/nx-parallel/pull/114)**

1. Added a list for running undirected graphs, so we don't have to change the graph type everytime when running a func.
2. Default graph type to undirected graphs.
3. Re-checked for any scope for improvement.
4. Tested across various types of functions.


### Re-check all of the work done for potential improvements
**Duration: [4 hours]** </br>

- `number_` algorithms - ready
- `is_reachable` with numpy - ready
    - reverted changes to the timing script
- make `n_jobs=-1` - ready
    - read through the PR, aligned a few redundant lines and verified everything.
- `should_run` - ongoing
    - Refined the docstrings
    - The current tests did not go well with the decorator approach.
    - I tried to add new tests but I encountered errors related to number of jobs used.
    - Brainstormed different ways to add tests.
    - WIP: adding a single test for each `should_run_policy` function.


I’ve been a bit sick so I haven't been at my productive best so far. I’ll make it up over the week. Thank you for understanding :)



