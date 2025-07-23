## 23rd July
**Total Combined hours : 4.5 hours**

### Link Prediction algorithms 
**Duration: [3 hours]** </br>
**Associated PR:** [PR#127](https://github.com/networkx/nx-parallel/pull/127)

1. added community-based link prediction algorithms, which was straightforward to integrate.
2. added common neighbor centrality as well.
3. tested both against the timing script — observed 1.5–4× speedups over the standard version.
4. added benchmarks with a setup function:
    - for community based link prediction algorithms, you must explicitly assign community labels to nodes. Doing this inside the timed block would distort runtime measurements, so the setup step pre-assigns communities instead.
5. one main issue that came up:
    - internal predict function is expected to raise errors lazily (when the generator is consumed). But since Parallel evaluates the chunks immediately, exceptions are raised eagerly instead — causing a few test cases to fail.
    - I'm still exploring how to keep the error raising lazy while running the computation in parallel. I’ll bring this up for discussion in tomorrow’s meeting.

End Result: It's still a WIP.

### Additional Work done
**Duration: [1.5 hours]** </br>

- added benchmarks for `number_` algorithms (ref. [PR#117](https://github.com/networkx/nx-parallel/pull/117))
- started writing the weekly blog.






