# [REPT: Reverse Debugging of Failures in Deployed Software](https://www.usenix.org/system/files/osdi18-cui.pdf)

###### Weidong Cui, Xinyang Ge, Baris Kasikci, Ben Niu, Upamanyu Sharma, Ruoyu Wang, Insu Yun

---

### What is the Problem? [Good papers generally solve *a single* problem]

Debugging failures in deployed systems is known to be difficult since developers have to rely on limited information and execution history is generally unavailable.

### Summary [Up to 3 sentences]

REPT enables software failure reverse debugging in deployed systems. REPT utilizes hardware traces to record a program’s control flow with low overhead and it also uses binary analysis to recover data flow information based on the logged information. As a result, REPT is capable of reverse debugging by combining the logged control flow and the recovered data flow.

### Key Insights [Up to 2 insights]

- To recover from irreversible instructions, REPT uses forward analysis to recover destroyed values as long as the destroyed values are coming from other registers (which values are available).
- In order to recover irreversible memory writes, REPT leverages its error correction (in the DFG) algorithm so that it infer memory values based on backward analysis.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- For performance reasons, though symbolic execution helps with data recovery, the constraints (for solving which inputs led to a specific failure) gathered in the process is too large for long traces. Instead it register/memory information at the instruction positions.
- REPT handles concurrency on multi-core systems by using timing logs in hardware traces then recognize memory writes that affect data recovery. REPT divides simultaneous execution of multiple instructions into one conceptual instruction and see if changes in ordering of 2 concurrent subsequences would affect value of a specific memory location in order to eliminate impact induced by ambiguous ordering of subsequences.

### Limitations/Weaknesses [up to 2 weaknesses]

- The tradeoff of online logging and offline recovery is an open question; which in this case, control flow traces may be insufficient to capture bugs for offline recovery.
- Evaluation of REPT is mostly focused on single machine tests. Distributed systems on the other hand, usually uses event logging and we can yet see how program tracing could be baked into the debugging flow of such systems.

### Summary of Key Results [Up to 3 results]

- REPT is a way of reverse debugging for deployed systems and it allows accurate and efficient data recovery based on a control flow trace and a memory dump by performing forward and backward execution iteratively with error correction.
- REPT achieves high accuracy data recovery on real-world open-source applications unless instructions involve a hugh amount memory allocations.
- Overhead incurred in hardware tracing and offline analysis are very low even in consumer-level machines.

### Open Questions [Where to go from here?]

- How would data races complicate record/replay techniques such that REPT only opted for control flow tracing and utilizing memory dumps?
