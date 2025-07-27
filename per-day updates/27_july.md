## 18th July
**Total Combined hours : 6.5 hours**

### Added a section in test_get_chunks for community based link prediction algorithms
**Duration: [3.5 hours]**
**Associated PR**: [PR#127](https://github.com/networkx/nx-parallel/pull/127)

1. Modified `_apply_prediction` to return generators.
2. Confirmed reasoning for the errors obtained in link prediction algorithms.
    - early calling of exceptions before `pytest.raises`
    - no order to the generator after consumption
    - no community assignment in nodes.
3. Ensured that they passed test by adding tests to test_get_chunks
4. Read a bit about pytest.raises on https://docs.pytest.org/en/7.1.x/how-to/assert.html.
5. Identified pain points in the tests running in Networkx which would need modification.
6. Documented these updates in the PR.

End Result: Raised [PR#129](https://github.com/networkx/nx-parallel/pull/129) that adds a test to tackle community based link prediction algorithms 

### Published bi-weekly blog
**Duration: [1 hour]**

- Finalised the blog and added the latest updates to it.

### Understanding why parallel processes can be slow sometimes:
**Duration [2 hours]**

1. Read through : https://joblib.readthedocs.io/en/latest/parallel.html#serialization-processes
    - loky backend relies on cloudpickle for serialising
    - tried switching to multiprocessing but it seems unable to handle local predict function (i.e Can't get local object '_apply_prediction.<locals>._process_pair_chunk'). 
    - did not get different results after trying out multiprocessing backend and making sub-function global as well (became worse in fact)
2. Briefly read through: https://stackoverflow.com/questions/65026499/why-does-joblib-parallel-execution-make-runtime-much-slower
    - bottleneck revolves around serialising arguments?
3. obtained a basic understanding of time taken in parallel by turning on verbose whereas serial here takes 0.006s.
    ```bash
    [Parallel(n_jobs=8)]: Using backend LokyBackend with 8 concurrent workers.
    [Parallel(n_jobs=8)]: Done   1 tasks      | elapsed:    0.2s
    [Parallel(n_jobs=8)]: Done   2 out of   8 | elapsed:    0.2s remaining:    0.6s
    [Parallel(n_jobs=8)]: Done   3 out of   8 | elapsed:    0.2s remaining:    0.4s
    [Parallel(n_jobs=8)]: Done   4 out of   8 | elapsed:    0.2s remaining:    0.2s
    [Parallel(n_jobs=8)]: Done   5 out of   8 | elapsed:    0.2s remaining:    0.1s
    [Parallel(n_jobs=8)]: Done   6 out of   8 | elapsed:    0.2s remaining:    0.1s
    [Parallel(n_jobs=8)]: Done   8 out of   8 | elapsed:    0.3s finished
    0.26879072189331055
    ```
4. Look into more of this :)