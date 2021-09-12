# [Exokernel:An Operating System Architecture for Application-Level Resource Management](https://pdos.csail.mit.edu/6.828/2016/readings/engler95exokernel.pdf)

###### Dawson R. Engler, M. Frans Kaashoek, and James O’Toole Jr

---

### What is the Problem? [Good papers generally solve *a single* problem]

This paper attempts to come up with a prototype that allows applications to control machine resources in ways not possible in a traditional
operating system. The observation for coming up with such solution is that traditional operating systems attempt to provide all features for all applications, which incurrs unnecessary overhead and prevents application-specific optimizations.

### Summary [Up to 3 sentences]

Extending from the end-to-end argument paper, the author believes that the applications should know better than operating systems what the goal of their resource management decisions should be. Hence the exokernel implementation allows traditional abstractions to be implemented at the software level -- conflicts between the application and the abstractions can be resolved without intervention of kernel architects, which increases generality and promotes innovation.

### Key Insights [Up to 2 insights]

- The author proposed 3 major design principles for the exokernel: (1) Secure binding, (2) Resource revocation and (3) Abort protocol. These elements achieve (1) tracking resource ownership, (2) ensuring protection of resource usage and (3) revoking access for unresponsive applications -- fulfilling the ultimate goal of providing maximum freedom to library OS while maintaining protection.
- The paper provided an implementation of the exokernel (Aegis) which provides context of how these major design principles benefit performance.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- Starting from base costs, the author gave concrete explanations on how Aegis handles various operations so that it is faster than Ultrix in orders of magnitude. The combination of time slices, initiation/termination upcalls, and directed yields allows for faster inter-process communication.
- The author presented an example of a LibOS (ExOS) which demonstrated how fast interprocess communication is by performing experiments pertaining to measuring the latency of sending information from one process to another; also the cost of crossing the kernel and user space is extremely low which complements the implementation of optimizations of libraries at the application level -- ASHs, for example, defer buffer binding decisions until receving a msesage and use application-level data structures and system state to determine message placement. ExOS also effectively schedules a list of processses by stride scheduling with the help of Aegis's yield primitive. 

### Limitations/Weaknesses [up to 2 weaknesses]

- If virtual memory and the file system are completely at application level, the exokernel may be unable to distinguish pages used to cache disk blocks and pages used for virtual memory.

### Summary of Key Results [Up to 3 results]

- All functionality necessary for protection resides in the exokernel, control over hardware resources is handed to applications.
- An exokernel, unlike a traditional OS, is  (1) unprivileged, and (2) modifiable and deployable by orders of magnitude due to the nature of being close to the application-level.

### Open Questions [Where to go from here?]

- Interfaces at the application-level must offer the protection such that one libOS can assure high-level abstractions, leaving the burden to application-end developers -- which may be an undesirable trait for application development given how operating systems evolve nowadays.
