# [Learning from Mistakes — A Comprehensive Study on Real World Concurrency Bug Characteristics](https://www.cs.columbia.edu/~junfeng/09fa-e6998/papers/concurrency-bugs.pdf)

###### Shan Lu, Soyeon Park, Eunsoo Seo and Yuanyuan Zhou

---

### What is the Problem? [Good papers generally solve *a single* problem]

This paper addresses the challenge of writing concurrent programs which requires concurrency detection and concurrency programming models. And tries to offer a comprehensive review on characteristics of concurrency bugs.

### Summary [Up to 3 sentences]

The authors provided the a comprehensive real world concurrency bug characteristic study to examine the bug patterns, manifestations, fix strategies and other characteristics of real world concurrency bugs. For each bug, the authors carefully examined its bug report, corresponding source code and related patches, all of which together provide us a relatively thorough understanding of the bug patterns, manifestation conditions, fix strategies and diagnosis processes.

### Key Insights [Up to 2 insights]

- Intuitively, it is common for programmers to assume a certain order between two operations from two threads. Specifically, programmers would assume (1) between a write and a read to one variable; (2) between two writes to one variable. For example, programmers might expect Statement 1 (younger) to initialize io pending before Statement 2 (older) assigns a new value to it. However, the execution of the asynchronous read can be very quick and Statement 2 may be executed before Statement 1, contrary to the expectation of programmers. This makes thread 1 to hang.
- Since programmers think in the context sequentially, it is probably straightforward to assume that small code regions will be executed atomically. For example, programmers assume that if Statement 1 reads a non-NULL value from process information, Statement 2 will also read the same value (Both Statements are run on the same thread). However, such an atomicity assumption can be violated by Statement 3 (Which happens in between of Statement 1 and Statement 2) during concurrent execution, and it crashes the program.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- Since most threads don't closely interact with each other all that often, and that most communication and collaboration is conducted between a small group of threads, we can conclude that concurrent program testing can pairwise test program threads, which reduces testing complexity without losing bug exposing capability much.
- One out of all deadlock bugs is triggered by three threads circularly waiting for three resources, hence deadlock-oriented concurrent program testing can pairwise test the order among acquisition and release of two resources.

### Limitations/Weaknesses [up to 2 weaknesses]

- The analysis can extend further to contain bug-detection tools that is capable of identifying bugs of multi-varient.

### Summary of Key Results [Up to 3 results]

- Based on 105 concurrency bugs, the authors found many implications for concurrency bug detection, testing and concurrent programming language design.
- The author also explored transactional memory (TM) for concurrency bug avoidance and in their comprehensive analysis on whether TM can ease the burden of expressing synchronization intentions in the exact manner, which avoids a big portion of concurrency bugs.

### Open Questions [Where to go from here?]

- How does better language features to support “order” semantics to further ease concurrent programming?
