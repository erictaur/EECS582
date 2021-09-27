# [Xen and the Art of Virtualization](https://www.cl.cam.ac.uk/research/srg/netos/papers/2003-xensosp.pdf)

###### Paul Barham, Boris Dragovic, Keir Fraser, Steven Hand, Tim Harris, Alex Ho, Rolf Neugebauer, Ian Pratt, Andrew Warfield


---

### What is the Problem? [Good papers generally solve *a single* problem]

Previous systems do not fully support performance isolation such that the scheduling priority, hardware resource utilization, network traffic and disk accesses of one process impact the performance of others.

### Summary [Up to 3 sentences]

Xen multiplexes physical resources at the granularity of an entire operating system and is able to provide performance isolation between them. And it utilizes paravirtualization which reduce the portion of the guest's execution time spent performing operations which are substantially more difficult to run in a virtual environment compared to a non-virtualized environment.

### Key Insights [Up to 2 insights]

- The hypervisor itself in Xen provides only basic control operations. These operations are exported through an interface accessible from authorized domains. Complex policy decisions are best performed by software running over a guest OS rather than in privileged hypervisor code
- In order to achieve the best possible performance when virtualizing x86 architectures, all valid page translations for the current address space should be present in the hardware-accessible page table. Moreover, context switching typically require a complete TLB flush since the TLB is not tagged. Two design decisions for Xen were made accordingly: (i) guest OSes are responsible for managing the hardware page tables, with minimal involvement from Xen; and (2) Xen exists in a 64MB section at the top of every address space, thus avoiding a TLB flush.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- A circular queue of descriptors allocated by a domain and is also accessible from within Xen. Access to the circular queue is based around two pairs of producer-consumer pointers.
- The paper improved the performance of system call exceptions: increase system calls performance by allowing each guest OS to register an exception handler which is accessed directly by the processor without indirecting via ring 0 (hypervisor).

### Limitations/Weaknesses [up to 2 weaknesses]

- Due to different ring permissions, it is not possible to apply the same method used in system calls to the page fault handler because only code executing in ring 0 can read the faulting address from register CR2; page faults must therefore always be delivered via Xen so that this register value can be saved for access in ring 1.

### Summary of Key Results [Up to 3 results]

- Xen overcomes the inability to host transient servers for short periods of time and with low instantiation costs.
- In contrast to process-level multiplexing, Xen allows a range of guest OS to gracefully coexist rather than mandating a specific application binary interface.

### Open Questions [Where to go from here?]

- Is it possible implement a shared buffer indexed on block contents? Different domains could share data without sacrificing isolation.
