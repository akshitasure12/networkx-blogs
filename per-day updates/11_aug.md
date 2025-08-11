## 11th Aug
**Total Combined hours : 5.5 hours**

### support target parameter for `generate_random_paths`
**Duration: [3 hours]** </br>
**Associated issue: [Issue #8014](https://github.com/networkx/networkx/issues/8014)**

1. Browsed through ongoing issues in NetworkX.
2. Understand [PR#8002](https://github.com/networkx/networkx/pull/8002#discussion_r2062660325), read through the discussion, check the changes made, previous implementation, familiarise myself with `generate_random_paths`.
3. Read discussion under [issue #8014](https://github.com/networkx/networkx/issues/8014).
4. After reading through and understanding, I think I agree with Ross in [comment](https://github.com/networkx/networkx/issues/8014#issuecomment-3061789527) that it's better to let the users be explicit about what they want.
5. So, after the example suggested, it made more sense to not add the target option imo.

End Result: Learning and Experimentation

### Degree Centrality-- open PR
**Duration: [1 hour]** </br>
**Associated PR: [PR#98](https://github.com/networkx/nx-parallel/pull/98)**

1. Earlier, I had begun reading the comments, but today I observed that the NetworkX implementation and the implementation in this branch differed.
2. I delved into it and realised that the entire function computed centrality values for a set of nodes on top level with simple multiplication.
3. I had already begun making modifications to this PR, but then overall since it was just multiplication-- I did not proceed further.


### Refactor Parallel Graph Algorithms to Use a Centralized Parallel Configuration-- Open PR
**Duration: [1.5 hours]** </br>
**Associated PR: [PR#86](https://github.com/networkx/nx-parallel/pull/86)**

1. It was a great idea, considering that after implementing so many algorithms, the initial steps were redundant.
2. Went through the commits.
3. Understood the flow of the PR.
4. Since, it was open for time now, I noticed areas where there could be improvements and updates:
    - Betweeness centrality empty graph case
    - The test files etc. have been modified, a lot in chunk.py

End Result: It seemed like a better idea to confirm with mentors if I could work on this simultaneously or just add review comments on the current PR.