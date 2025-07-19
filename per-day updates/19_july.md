## 18th July
**Total Combined hours : 5 hours**

### Compared benchmarks of nx-parallel vs Networkx
**Duration: [4 hours]** </br>
**Associated PR**: [PR#119](https://github.com/networkx/nx-parallel/pull/119)

1. Used [asv docs](https://asv.readthedocs.io/en/stable/asv.conf.json.html) to debug the numpy import error.
2. Read through [PR#24](https://github.com/networkx/nx-parallel/pull/24).
3. Learnt that a different benchmark strategy is used for NetworkX (a setup function) and nx-parallel (uses cached graph).
4. Documented thse findings with the help of an issue.
5. Tried to debug how we were getting the speedups by experimenting by understanding `n_jobs` used, which kept resulting in None.
6. Ran benchmarks for different commits to see if expected results match the outcome to get a better idea (tweaked number of nodes, experimented with different x-axes)
7. Tested benchmarks for pure python implementation vs Networkx implementation of is_reachable() 
8. Tested benchmarks for numpy implementation vs Networkx implementation of is_reachable()

End Result: 
- Raised [Issue #125](https://github.com/networkx/nx-parallel/issues/125) for creating uniform benchmarks using setup function.
- Added the speedup benchmarks received after testing in the associated PR along with a few unresolved doubts.

### Addition changes made:
**Duration: [1 hour]**

1. Updated my PR on harmonic centrality by documenting the optimisation used (to avoid redundant set creation) in [PR#124](https://github.com/networkx/nx-parallel/pull/124).

2. Updated CONFIG.md and README.md for final touches in [PR#122](https://github.com/networkx/nx-parallel/pull/122). Changed it from a draft PR to ready for review state.

### Note for mentors:
PRs ready for review:
- [PR#106](https://github.com/networkx/nx-parallel/pull/106)
- [PR#117](https://github.com/networkx/nx-parallel/pull/117)
- [PR#122](https://github.com/networkx/nx-parallel/pull/122)



