## 31st July
**Total Combined hours : 3 hours**

1. Documented respective updates in the meeting notes along with a few doubts in mind.
2. Tried working with `average_clustering` which had 3 ways of implementation:
    - should we use NetworkX's `clustering` implementation and parallelise sum, len functions in `average_clustering`?
    - should we simply use parallel `clustering` in `average_clustering`?
    - should we use parallel `clustering` and also parallelise sum, len functions in `average_clustering`?
    - benchmarked the first 2 ways and it seems like we would not need to parallelise `average_clustering` itself since they are light weight computations.
3. Addressed the review comments in [PR#8170](https://github.com/networkx/networkx/pull/8170).