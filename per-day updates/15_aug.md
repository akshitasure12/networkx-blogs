## 15th Aug
**Total Combined hours : 5 hours**

### Timing Script
**Duration: [2.5 hours]** </br>

1. Updated README.md with latest heatmaps.
2. Added machine specifications etc. 
3. Ran timing script for a few algorithms:
    - edge_betweenness_centrality
    - approximate_all_pairs_nodes_connectivity
4. Seggregated new and old heatmaps as per the comments received.


### Timing Script
**Duration: [2.5 hours]** </br>

1. Used dag instead of a directed graph in benchmarks and `test_get_chunks.py`
2. checked what the available dag options for graphs are:
    - `gn_graph`
    - `path_graph`
    - Path_graph would not be randomised so I chose `gn_graph`.
3. Verified the timing scripts for both path_graphs and gn_graphs.
4. Updated PR to pass tests (rebased).
5. Updated `test_get_chunks` with another list which was missed due to the use of a directed graph instead of a dag.




