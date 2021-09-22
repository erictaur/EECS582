# [AutoFDO: Automatic Feedback-Directed Optimization for Warehouse-Scale Applications](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/45290.pdf)

###### Dehao Chen, David Xinliang Li, Tipp Moseley

---

### What is the Problem? [Good papers generally solve *a single* problem]

Current FDO models are not commonly used due to (1) runtime overhead during profile collection, (2) tedious dual-compile usage model, and (3) difficulties in generating a representative training data set.

### Summary [Up to 3 sentences]

AutoFDO skips the instrumentation step and instead uses sampling based profile to drive feedback directed optimizations. First it generates the necessary profiles by logging events in the processor then proceed to inlining preperation and annotate block frequencies.

### Key Insights [Up to 2 insights]

- The symbolization service (Binary’s Build-ID serves as a globally unique identifier) incurs low overhead while making debugging easier for developers when symbolizing all of the samples observed for a single binary. 
- The paper lists the source of profile inaccuracies such as benign transformations and Unrecoverable destructive changes and how proposed algorithms mitigate the shortcomings

### Notable Design Details/Strengths [Up to 2 details/strengths]

- Profile sampling can occur on production systems and profiles shall therefore be available for FDO builds without the need for any special instrumentation build.
- Profiled data sampled during testing phases can then be used to build the optimized binary with low overhead.

### Limitations/Weaknesses [up to 2 weaknesses]

- Some applications that lack in tuning would not benefit from AutoFDO or FDO in general.
- Some optimizations affect debug information, which prevents the same optimization from happening in the next iteration.

### Summary of Key Results [Up to 3 results]

- FDO is usually most effective on applications that many function calls and biased branches the compiler cannot statically predict -- which actually is a large fraction of Google’s entire software footprint
- The source location representation triplet can effectively tolerate file name/path changes, and can also lock the source change within a function. But the paper stlil provides recovery for users to recover from potential performance loss due to a stale profile.

### Open Questions [Where to go from here?]

- How to improve profile quality by enhancing the discriminator to record cloned/duplicated instructions?
