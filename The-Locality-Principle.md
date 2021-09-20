# [The Locality Principle](http://denninginstitute.com/pjd/PUBS/CACMcols/cacmJul05.pdf)

###### Peter J. Denning

---

### What is the Problem? [Good papers generally solve *a single* problem]

The first adoptations of virtual memory boosted performance by threefold or more, but performance is very reliant on page replacement policies, which lead to thrashing in a multi-programming environment that attempted to saturate core utilization. The locality principle allowed the emergence of the replacement algorithms and compilers we see today.

### Summary [Up to 3 sentences]

By observing the fact that a process’s working set of pages can be thought as a collective group of pages used during a fixed-length sampling window; the author proposed a feedback control mechanism that would limit the multiprogramming by refusing to activate programs that have a working set that exceeds the size of main memory.

### Key Insights [Up to 2 insights]

- The emergence of thrashing was counterintuitive since system performance plummeted at low utilization.
- The idea of a working set is a justified notion of assuming pages seen in main memory is either temporally or spatially close in distance.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- Temporal clustering can be seen due to looping and executing within local data (i.e. function calls); and spatial clustering is observed due to related values being grouped into a common data structure (i.e. vectors)
- Virtual memory harnessed locality to measure dynamic memory demand for different processes and adapt the memory allocation to avoid thrashing

### Limitations/Weaknesses [up to 2 weaknesses]

- It would be cool to see how the CPU scheduler would behave after setting the constraint of the feedback mechanism the author mentioned.
- Is locality a mere coincidence?

### Summary of Key Results [Up to 3 results]

- The locality principle not only applies in the operating systems domain, but also in other parts of the computer system as well (VM, networks, etc.)
- The observed phenomena in programming semantics provided the basis to claim that programming itself has the nature of locality sets.

### Open Questions [Where to go from here?]

- The author mentioned using locality principles to assist forensics in the future but the notion itself is quite vague; not sure if there is literature that builds upon this idea.
