### Made a new PR for harmonic centrality 
**Duration: [1.5 hours]**

1. Coding out the approach consistent with that of NetworkX.
2. Optimise the approach for processing each chunk without using set intersection.
3. tried to figure out why the parallelism is drastically slower than the serial impl.

    a. tested by setting a max_chunk_size if sources are small in number - did not yield much results

    b. did a performance test for different values of n_jobs.

End result: raised a PR but something to think about would be if the speed cannot be increased at all.
            
### Work on should_run tests 
**Duration [1.5 hr]**
    
1. Spent time looking back at the flow of `should_run`
2. checked `nx-cugraph` for references for tests
3. tried resolving multiple errors I ran into (attribute errors and assertion errors)
4. brainstormed a few tests and committed them

End result: I added the tests, will wait for a review to see if I am expected to write any more tests or if I'm missing something.

### Improve make `n_jobs=-1` 
**Duration [2 hrs]**

1. Went through https://peps.python.org/pep-0020/
2. Re-read [config.md](http://config.md) and [readme.md](http://readme.md) multiple times to get a grasp of the user perspective and made a few changes accordingly along with catering to mentors suggestions.

End result: _Ready for review_
    
### Started working on [Issue #8155](https://github.com/networkx/networkx/issues/8155)
**Duration [0.5 hour]**
- Familiarised myself with connected components in tournament graphs.
- Made a division of the benchmarks into 2 parts but I couldn't complete it today.

### Compare performance of `is_reachable` on nx_parallel and NetworkX
**Duration [1 hour]**
- Added networkx backend to the asv benchmarks to compare.
- Constantly ran into a numpy import error.

    a. I tried adding numpy as a dependency into pyproject.toml assuming that would work but I'm not sure if thats the right way to go about it.

### Note for mentors:
- [PR#117](https://github.com/networkx/nx-parallel/pull/117), [PR#106](https://github.com/networkx/nx-parallel/pull/106) are both ready from my end.