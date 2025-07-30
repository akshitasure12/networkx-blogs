## 29th July
**Total Combined hours : 5 hours**

### Adding a clustering functionality
**Duration: [4 hours]** </br>
**Associated PR: [PR#130](https://github.com/networkx/nx-parallel/pull/130)**

1. Finalised the algorithm implementation and timed it.
    - The results of this equalled the time taken by the sequential implementation, no matter how many workers I added.
2. Above, made me realise I was going about it in an incorrect manner.
    - All of the heavy lifting was done sequentially so the parallelism was in vain.
3. I modified the function to do the heavy lifting across cores.
4. Dealt with `AssertionError` for singleton returns and `TypeError` for non-iterable `int` inputs.
5. I tried running it for a bit but it kept taking extremely long time to run (1/2 hr for 800 nodes and 1 edge probability).
6. referred to [collections section](https://docs.python.org/3/library/collections.abc.html#collections.abc.Iterable) in python documentation for iterable check.
7. Added the benchmarks and tested the algorithm.
8. Tried implementing `average_clustering` as well that uses `clustering` but this would require some more thought as to how we can handle inner parallel calls.

End result: Raised [PR#130](https://github.com/networkx/nx-parallel/pull/130) that implements clustering.


### Addressed PR comments 
**Duration: [1 hour]** </br>

1. module naming heirarchy in [PR#128](https://github.com/networkx/nx-parallel/pull/128)
2. using a generator in [PR#127](https://github.com/networkx/nx-parallel/pull/127)