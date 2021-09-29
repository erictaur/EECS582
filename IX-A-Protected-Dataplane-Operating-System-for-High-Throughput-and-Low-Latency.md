# [IX: A Protected Dataplane Operating System for High Throughput and Low Latency](https://www.usenix.org/system/files/conference/osdi14/osdi14-paper-belay.pdf)

###### Adam Belay, George Prekas

---

### What is the Problem? [Good papers generally solve *a single* problem]

Hardware resources in modern computer systems nowadays should allow for low latency for datacenter applications but commodity operating systems have been designed under very different hardware assumptions.

### Summary [Up to 3 sentences]

 IX is a dataplane operating system that leverages hardware virtualization to isolate the Linux control plane and the IX dataplane instances that implement in-kernel network processing and the applications running on top of them.

### Key Insights [Up to 2 insights]

- IX separates the control of the kernel, responsible for resource configuration, provisioning, and scheduling from the dataplane, which runs the networking stack and applications.
- The implementation used network adapters (NIC) with receive-side scaling to provide hashing of incoming traffic to distinct hardware queues. Each hyperthread serves a single receive and transmit queue per NIC, hence eliminating the need for synchronization traffic between cores in the network stack.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- Each dataplane operates as a single address-space OS and supports two thread types within a shared address space: (i) elastic threads which interact with the IX dataplane to initiate network I/O and (ii) background threads. The allocated hardware threads can be timeshared to be different threads.
- A malicious or misbehaving application can only hurt itself and it cannot corrupt the networking stack or affect other applications: Applications cannot access dataplane memory, except for read-only message buffers.

### Limitations/Weaknesses [up to 2 weaknesses]

- Experiments show that a hardware limitation that was triggered at high packet rates with small average batch sizes (But fixed with coalesced writes)

### Summary of Key Results [Up to 3 results]

- IX dataplane provides a native, zero-copy API that explicitly exposes flow control to applications
- IX dataplane is optimized for multi-core: elastic threads operate in a synchronization and coherence free manner in the common case. 

### Open Questions [Where to go from here?]

- The performance properties analyzed by the Mystery machine are fairly high-level. One interesting direction would be to extend this work to gather more information in a targeted way to do more low-level performance debugging (e.g., what code is responsible for the slow down?).
