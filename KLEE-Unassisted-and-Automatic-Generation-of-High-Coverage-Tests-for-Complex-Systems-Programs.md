# [KLEE: Unassisted and Automatic Generation of High-Coverage Tests for Complex Systems Programs](https://llvm.org/pubs/2008-12-OSDI-KLEE.pdf)

###### Cristian Cadar, Daniel Dunbar, Dawson Engler

---

### What is the Problem? [Good papers generally solve *a single* problem]

Symbolic execution has concerns of the ability to consistently achieve high coverage on real applications. 

### Summary [Up to 3 sentences]
KLEE is a symbolic execution tool that automatically generated tests that has exceeded 90% line coverage with no compromise in constraint accuracy. KLEE can also get significantly more code coverage than a concentrated, sustained manual effort and is not limited to low-level programming errors.

### Key Insights [Up to 2 insights]

- KLEE directly interprets programs compiled to LLVM assembly, and maps instructions to constraints without approximation. By tracking memory objects, KLEE read-modify-writes objects so that it reduces state memory.
- KLEE selects the state to run at each instruction by interleaving Random Path Selection (maintains a binary tree recording the program path followed for all active states) and Coverage-Optimized Search (select states likely to cover new code in the immediate future by computing a weight for each state).

### Notable Design Details/Strengths [Up to 2 details/strengths]

- Even for small (short) programs, the complexity of intricate control flowm boundary conditions and testing out all important environment dependencies is not trivial; KLEE tries to hit all lines in the code and detect dangerous operations buy running the program symbolically (operate on constraints rather than values)
- KLEE simplifies the constraint set by rewriting previous constraints when new equality constraints are added to the constraint set, which is a utilization of nature of operation on variables in a program.

### Limitations/Weaknesses [up to 2 weaknesses]

- Still not really applicable to any arbitrary program with non-deterministic behavior. 

### Summary of Key Results [Up to 3 results]

- KLEE test cases can be run on the raw version of the code which simplifies debugging and error reporting.
- KLEE constraints does not compromise any accuracy. If the KLEE constraint solver is unable to violate an assert, then the current path is proven to be error-prone for this specific assertion.

### Open Questions [Where to go from here?]

- How does this compare to hardware formal verification? It seems that the clever optimizations in KLEE can overcome the exploding state space.
