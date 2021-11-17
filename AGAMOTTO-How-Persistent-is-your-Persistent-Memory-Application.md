# [AGAMOTTO: How Persistent is your Persistent Memory Application?](http://web.eecs.umich.edu/~twenisch/papers/osdi14.pdf)

###### Ian Neal, Ben Reeves, Ben Stoler, Andrew Quinn

---

### What is the Problem? [Good papers generally solve *a single* problem]

Testing effort on PM systems has low bug coverage as it relies primarily on extensive test cases and developer annotations. Existing PM testing do not identify application-independent patterns of misuse, and therefore require annotations to detect bugs.

### Summary [Up to 3 sentences]

AGAMOTTO is an extensible system that leverages symbolic execution for discovering misuse of persistent memory in PM applications and with the incoporated symbolic memory model it is able to constitute whether PM state has been made persistent. The state exploration algorithm used in AGAMOTTO allow it to direct the system to code that is susceptible to persistency bugs.

### Key Insights [Up to 2 insights]

- AGAMOTTO does not have to rely on user annotations or an extensive test suite and detect bugs using two universal persistency bug oracles automatically. Extended bug oracles also allow detection of application-specific bugs.
- The paper provided a comprehensive study on persistency bugs on PM systems. It noted that the missing flush/fence patterns such that a pointer to persistent memory is not flushed when under certain branch situations and would lead to rogue writes or malformed data reads.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- During state space exploration, oracles in AGAMOTTO detect bugs relies on AGAMOTTO's symbolic execution engine to invoke a constraint solver and determine the inputs that led to the bug, thereby creating a test case that a developer can use for debugging.
- The universal persistency bug oracles in AGAMOTTO identifies an irrelevant flush/fence operation bug on all flushes to a cache-line which must already be pending/clean based on
the constraints on the persistent state. AGAMOTTO also identifies extraneous flush/fence bugs on all fences which has no pending flushes to mark clean.

### Limitations/Weaknesses [up to 2 weaknesses]

- In some cases of application-specific code, AGAMOTTO is potentially unable to discover bugs in other testing platforms if execution of the kernel is part of the application.

### Summary of Key Results [Up to 3 results]

- According to the evaluation in the paper, AGAMOTTO’s state exploration strategy can expose bugs very quickly and may even be a viable option for interactive debugging; which proved AGAMOTTO’s state exploration strategy to be effective.
- The overhead of static analysis in AGAMOTTO is low relative to the length of time spent on discovering bugs compared to platforms that link with external libraries.
