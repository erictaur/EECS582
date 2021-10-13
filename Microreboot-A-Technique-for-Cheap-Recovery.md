# [Microreboot – A Technique for Cheap Recovery](https://www.usenix.org/legacy/event/osdi04/tech/full_papers/candea/candea.pdf)

###### George Candea, Shinichi Kawamoto, Yuichi Fujiki, Greg Friedman, Armando Fox

---

### What is the Problem? [Good papers generally solve *a single* problem]

There is no previous methodology that is able to surgically recover faulty applications without disturbing other componenets.

### Summary [Up to 3 sentences]

By completely separating process recovery from data recovery, and delegating the recovery to specialized state stores, the use of microreboots to achieve process recovery with less downtime and cost.

### Key Insights [Up to 2 insights]

- A crash-only approach allows for robust programming in terms of (1) partitioning a system into components for short start time and also benefits the programmer (2) segregating recovery of persistent data from application logic can improve the recoverability of both the application and the data and (3) inter-component interactions in a crash-only system ideally use timeouts and, if no response is received to a call within the allotted time frame, the caller can gracefully recover.
- Resources in a frequently-microrebooting system should be leased, to improve the reliability of cleaning up and prevent resource leaks.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- The reason for choosing J2EE as the prototype platform is because EJBs (portable components of applications) provide a level of componentization that is suitable for building crash-only applications. It destroys all extant instances of the corresponding EJBs, kills threads associated with those instances and releases all associated resources and then reinstantiates.
- In their implementation, preservation of state across microreboots and the segregation of session state in eBid offers recovery decoupling. Data shared across components by means of a state store frees the components from having to be recovered together.

### Limitations/Weaknesses [up to 2 weaknesses]

- Microreboots are not so effective against faults outside the application (OS/hardware level faults in registers and bad system calls, memory leaks, etc. require to restart JVM)
- Microreboot does not scrub data that is maintained by the application and it also erases volatile shared state regardless of correctness.

### Summary of Key Results [Up to 3 results]

- EJB level microrebooting is effective against failures that mostly constituent in most J2EE applications and is faster in terms of recovery and reduces functional disruption.
- As seen in the observations, microrebooting results in less failed requests and fraction of failed requests stayed rather constant regardless of cluster size. 

### Open Questions [Where to go from here?]

- Is there a way to recover from faults that occured below the application level? (Restart a kernel without affecting others?)
