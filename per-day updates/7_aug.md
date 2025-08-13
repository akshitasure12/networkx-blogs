## 7th Aug
**Total Combined hours : 3.5 hours**

### Got an idea to implement `_apply_pred`
**Duration: [1 hour]** </br>
**Associated PR: [PR#129](https://github.com/networkx/nx-parallel/pull/129)**

1. Running `_apply_pred` using generators alone.
2. Tried fixing "UserWarning: 16 tasks which were still being processed by the workers have been cancelled. You could benefit from adjusting the input task iterator to limit unnecessary computation time."
3. Incorrect results obtained so I reverted the changes.
4. Used this PR as an inspiration to see if it could result in anything different: https://github.com/networkx/nx-parallel/pull/14

### Went through all the previously closed PRs
**Duration: [2.5 hours]** </br>

1. Spent time reading old PRs to see if there are other areas that I can cover.
2. Brainstormed and explored other ways of implementing `test_get_chunks`
    - ref. https://github.com/networkx/nx-parallel/pull/63/files#r1608495035

