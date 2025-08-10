## 8th Aug
**Total Combined hours : 7.5 hours**

### Work on `test_get_chunks`
**Duration: [4.5 hours]** </br>
**Associated PR: [PR#129](https://github.com/networkx/nx-parallel/pull/129)**

1. I was trying to implement an optimal approach for `test_get_chunks`
2. Compiled all the changes that I made to `test_get_chunks` in different PRs to a single one.
3. I initially followed the approach to try and make independent functions in `test_get_chunks` for cases when a generator is returned or a list or integers etc.
4. Later I realised that all of these cases were only used a single time so we could just add them directly to if-elde blocks.
5. Added a common list for directed graphs in specific which was not accomodated.
6. Different lists were being used which made it seem like it was hard-coded for each:
    - dag 
    - check_dict_values_close
    - requires_node_community 
    - not_implemented_undirected 
    - sep tournament functions
7. I got them down to use 4 lists for different graph types and worked on the code redundancy.
8. I spent some time trying to accomodate different edge-cases into the try-except block for better handling.
9. Revert back changes from different PRs to create a centralised `test_get_chunks` PR.
10. Tackle assertion errors, value errors (based on values returned by lists) and cases where I had wrongly used `sorted()` for integers.
11. Handled empty generator errors.
12. Ran the required changes across each PR to keep validating the success.
13. Document findings in the PR.

End Result: Updated the existing PR with the latest functionality.

### Additional work done
**Duration: [2 hours]** </br>

1. The heatmaps used a version of the timing script that isn't a part anymore, so I regenerated the respective heatmaps for `number_` algos in [PR#117](https://github.com/networkx/nx-parallel/pull/117).
2. Gathered all the information for the work done in the last 2 weeks-- to make a first draft of the biweekly blog.
3. Went through open PRs that I raised to check if I've missed out anything-- keep a track of the To Dos.


### Work on Degree Centrality-- open PR
**Duration: [1 hour]** </br>
**Associated PR: [PR#98](https://github.com/networkx/nx-parallel/pull/98)**

1. Rebased with the main after copying to a branch on my fork (resolving merge conflicts).
1. Read through all the commits of the PR.