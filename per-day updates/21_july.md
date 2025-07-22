## 21st July
**Total Combined hours : 3 hours**

### Link Prediction Algorithms
**Duration: [3 hours]** </br>
**Associated PR**: [PR#127](https://github.com/networkx/nx-parallel/pull/127)

1. Yesterday I had worked only on jaccard coefficient, today I added the remaining link prediction algorithms.
2. I tested them on the timing script and got speedups in 3 of the algorithms.
3. Recognised the overhead for `preferential_attachment` coz the internal predict function involved a simple computation (multiplication).
5. Returned a generator initially but that led to errors from `test_get_chunks` such as variation in order of the results obtained, `itertools.chain` object is not subscriptable. I debugged all those by returning a sorted list.
4. Link Prediction involves community algorithms, I can add these to link_prediction.py but before that I wanted to test it on different types of graphs and obtain the respective heatmaps. I didn't make much progress on this aspect today.

End Result: I raised a PR for this but it's still a work in progress.