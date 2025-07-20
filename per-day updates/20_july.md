## 20th July
**Total Combined hours : 7 hours**

### Harmonic Centrality
**Duration: [2 hours]** </br>
**Associated PR**: [PR#124](https://github.com/networkx/nx-parallel/pull/124)

1. Worked on the review comments regarding naming suggested, benchmarking using a setup function.
2. Raised a PR for harmonic centrality optimisation in networkx 
    - Documented what the optimisation is and uploaded relevant benchmarks to prove the improvement.
3. I also explored different ways to try and improve harmonic centrality to speed up:
    - Tried replacing the partial function (shortest path length) with `all_pairs_bellman_ford_path` for general cases where source and nbunch is not provided, but it only lead to worse complexities.
    - Recognised the most time consuming aspect to be passing the huge graph across cores.
    - Wasn't very successful. Although I was trying to see if memmapping could be incorporated here, still need to dig in.

End Result: 
- Raised [PR#8158](https://github.com/networkx/networkx/pull/8158) that adds discovered harmonic centrality code optimisations to Networkx (_Ready for Review_)
- WIP: Strategies to improve speed up

### Modified benchmarks to contain a setup function
**Duration: [1.5 hours]** </br>
**Associated PR**: [PR#126](https://github.com/networkx/nx-parallel/pull/126)

1. Read: https://asv.readthedocs.io/en/stable/writing_benchmarks.html
2. added the setup function with different graph objects for weighted and unweighted graphs.
3. Centralised the usage of seed across the benchmarks.

End Result:
- [PR#126](https://github.com/networkx/nx-parallel/pull/126): (_Ready for Review_)

### Parallel implementation of Link Prediction Algorithms
**Duration: [2 hours]** </br>

1. Made an inditial draft of the function.
2. Read through the joblib documentation to see if I could apply `return_as=generator` here but I didnt proceed with this approach because the output order woudn't be deterministic then.
3. Debugged exception not raised errors because I was returning a generator function and not a generator expression (like in Networkx).
4. I went into the rabbit hole of understanding pickling.
    - Why we need to pickle for multiprocessing?
    - Why generators dont support pickling? https://stackoverflow.com/questions/7180212/why-cant-generators-be-pickled helped me understand why.
So I ruled out the idea of returning a geenrator in the process chunk function.
5. Also went into details of why jaccard coefficient does not perform well for edge prob 1 based on the obtained heatmap.
    - `ebunch = nx.non_edges` but in case of edge probability 1, this would be empty. The parallel object and chunks would be created anyway in nx-parallel due to the lack of an early exit condition so I included one.

End Result:
- 90% done with the implementation along with obtaining speedups. Will raise a PR tomorrow :)

### Additional Review Comments I worked on
**Duration: [1.5 hours]** </br>

1. Worked on improving the logging explanation in [PR#122](https://github.com/networkx/nx-parallel/pull/122).
2. Incorporated PR comments on [PR#8158](https://github.com/networkx/networkx/pull/8158) wrt to benchmarks and early exit condition.
3. Re-ran benchmarks for [PR#119](https://github.com/networkx/nx-parallel/pull/119) to verify the previously obtained results,  documented the result and updated information in the respective PR.

### Note for mentors:
PRs ready for review: </br>
In nx-parallel:
- [PR#106](https://github.com/networkx/nx-parallel/pull/106)
- [PR#117](https://github.com/networkx/nx-parallel/pull/117)
- [PR#122](https://github.com/networkx/nx-parallel/pull/122)
- [PR#126](https://github.com/networkx/nx-parallel/pull/126)

In networkx: 
- [PR#8158](https://github.com/networkx/networkx/pull/8158)

