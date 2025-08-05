## 5th Aug
**Total Combined hours : 8 hours**

### 1. Re-open PR#74
**Duration: [6.5 hours]** </br>
**Associated PR: [PR#74](https://github.com/networkx/nx-parallel/pull/74)**

1. Rebase the old PR with the latest updates in nx-parallel and resolve merge conflicts.
2. Read the implementation of both algorithms in Networkx - [colliders](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.colliders.html) and [v_structures](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.dag.v_structures.html)
3. Read through the respective branch:
    - What changes have been made?
    - What all updates need to be made?
    - Understand each and every commit
4. Updated the code and refined it as per the methods followed in other algorithms.
5. Encountered errors in `test_get_chunks`, added a test for dag specific algorithms
    - **TO DO**: Research ways to implement `test_get_chunks` in a generic way maybe, instead of adding multiple conditionals.
6. Constant: zsh: killed     python3 timing/timing_individual_function.py
    - Tried to run it multiple times - but I believe it is due to memory leakage.
    - Solution: Generated heatmap for lesser number of nodes.
7. Tried different return types:
    - yielding a generator
    - returning a list faster than yielding
    (No success)
8. Try out mem-mapping for speedups : 
    - https://joblib.readthedocs.io/en/latest/parallel.html
    - errors fixed: returning numpy-scalars, assertion errors regarding nodes and their label mismatch
    (No speedups encountered as such)
    - too mnay values to unpack error
9. Investing why Timing script giving unreasonable 1.5x speedup for sequential vs paralle code with `n_jobs=1`
    - returning a list is faster than consuming a generator function into a list?

End Result: No approach paved a way to assure speedups for colliders.

### Additional Work:
**Duration: [1.5 hours]** </br>

1. Understand approach in https://github.com/networkx/networkx/pull/8167 that implements seperate benchmarks for `is_reachable()` to check if there are any comments I can help with?
2. Experiment ways to implement `test_get_chunks` in a general way instead of adding multiple if-else statements.
    - I think splitting into seperate tests instead of a monolithic one would be better..
3. Went through all the previous PRs to check if there could be any potential improvements or any comments that are yet to be accomodated.
