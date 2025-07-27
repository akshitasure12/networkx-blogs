## 18th July
**Total Combined hours : 4 hours**

### Added a section in test_get_chunks for community based link prediction algorithms
**Duration: [3 hours]**
**Associated PR**: [PR#127](https://github.com/networkx/nx-parallel/pull/127)

1. Modified `_apply_prediction` to return generators.
2. Confirmed reasoning for the errors obtained in link prediction algorithms.
    - early calling of exceptions before `pytest.raises`
    - no order to the generator after consumption
    - no community assignment in nodes.
3. Ensured that they passed test by adding tests to test_get_chunks
4. Read a bit about pytest.raises on https://docs.pytest.org/en/7.1.x/how-to/assert.html.

End Result: Raised [PR#129](https://github.com/networkx/nx-parallel/pull/129) to tackle community based link prediction algorithms

### Published bi-weekly blog
**Duration: [1 hour]**

- Finalised the blog and added the latest updates to it.

