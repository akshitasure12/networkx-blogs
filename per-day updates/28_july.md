## 28th July
**Total Combined hours : 6.5 hours**

### Adding a centralised `should_run` functionality
**Duration: [3 hours]** </br>
**Associated PR: [PR#123](https://github.com/networkx/nx-parallel/pull/123)

1. Added 2 helpers for `should_run` that each function's individual `_should_run` could call these.
2. But the redundancy problem was still prevalent. So, this approach had to be rejected.
3. I modified each decorator to pass the centralised `should_run` functions as arguments in the decorator.
4. Read this to grasp a better idea: https://www.freecodecamp.org/news/python-decorators-explained/
5. The overall implementation seems to be avoiding code duplication.
6. Modified test to accomodate tournament graphs.

End Result: Updated [PR#123](https://github.com/networkx/nx-parallel/pull/123) to a centralised `should_run`.

### Finalise `is_reachable()` 
**Duration: [2 hours]** </br>
**Associated PR: [PR#119](https://github.com/networkx/nx-parallel/pull/119)

1. test sequential against pure python implementation for speedups
    - speedups were not obtained (slow implementation)
2. test sequential against numpy implementation for speedups
    - speedups were not obtained (slow implementation)
    - performance better than that of pure python
    - utilising disk to read the graph instead of copying it and graph conversion done only once is not as expensive.
3. tried other minor optimisations
    - using `not any` instead of `all` for early exit etc.
4. pushed the updated heatmap
5. documented the respective changes in the PR.

End Result: In case of no other review comments, this PR would be ready.

### Addressed the review comments under `link_prediction.py`
**Duration: [1.5 hours]** </br>
**Associated PR: [PR#123](https://github.com/networkx/nx-parallel/pull/123)

1. tried using return_as='generator'
2. ran into errors like unable to raise nodeNotFound errors.
3. looked into concepts like returning a geenrator exp vs geenrator function
no conclusion yet :)

