# [The Multikernel: A new OS architecture for scalable multicore systems](https://people.inf.ethz.ch/troscoe/pubs/sosp09-barrelfish.pdf)

###### Andrew Baumann, Paul Barham, Pierre-Evariste Dagand

---

### What is the Problem? [Good papers generally solve *a single* problem]

It is no longer efficient to design/build a general-purpose OS for one or more particular hardware models: the deployed hardware varies wildly, and optimizations become obsolete after a few years when new hardware arrives. Optimizations in the design often involve tradeoffs in hardware parameters such as the cache hierarchy, memory consistency model, and relative costs of local and remote cache access so just the optimizations themselves are not portable between different hardware types.

### Summary [Up to 3 sentences]

Since multicore machines increasingly resemble complex networked systems, the authors proposed Barrelfish -- a multikernel architecture. Barrelfish is a distributed
system which may be amenable to local optimizations, rather than centralized system which must somehow be scaled to the networklike environment. By basing the OS design on replicated data, message-based communication, and split-phase operations, the authors applied knowledge from distributed systems and networking to the challenges posed by hardware trends.

### Key Insights [Up to 2 insights]

- Making inter-core communication (message passing) explicit allows operations that might require communication to be split-phase, by which we mean that the operation sends a request and immediately continues, with the expectation that a reply will arrive later. When requests and responses are decoupled, the core issuing the request can do useful work while waiting for the reply.
- Making replication of OS state intrinsic to the multikernel design makes it easier to preserve OS structure as underlying hardware evolves. The technique of replication also allows us to apply standard results from the distributed systems literature to maintaining the consistency of OS state across such changes.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- The authors factored the OS instance on each core into a privileged-mode CPU driver and a distinguished user-mode monitor process. CPU drivers are purely local to a core, and all inter-core coordination is performed by monitors. Since each driver does not share state with other cores, it is easier to write and debug than a conventional kernel, and enabling its data to be located in core-local memory incurs low overhead.
- Barrelfish uses a variant of user-level RPC (URPC) between cores, which is a region of shared memory used as a channel to transfer cache-line-sized messages point-to-point between single writer and reader cores. Message transports are abstracted behind a common interface, allowing messages to be sent/received in a transport-independent way. 

### Limitations/Weaknesses [up to 2 weaknesses]

- Barrelfish has yet to include other NIC topologies (multi/any cast protocols) on URPC transports. This might impact scalability.
- Current implementations are based on Intel/AMD multiprocessors which does not truly represent a heterogenous environment.

### Summary of Key Results [Up to 3 results]

- Despite the fact that up to 32 user-level processes are involved in each unmap operation, performance scales better than Linux or Windows, both of which incur the cost of serially sending IPIs. The large overhead on top of the baseline protocol is largely due to inefficiencies in the message dispatch loop of the user-level threads package.
- Barrelfish uses a distributed 2-phase commit operation for changing memory ownership and usage via capability retyping, which necessarily serializes more messages than TLB shootdown, and is consequently more expensive. Barrelfish still achieved good scaling and performance using the same multicast technique as with shootdown.

### Open Questions [Where to go from here?]

- How do we restructure the OS as a distributed system that allows us to closely matche the structure of some increasingly popular programming models for datacenter applications?
