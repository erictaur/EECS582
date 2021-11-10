# [Spanner: Google’s Globally-Distributed Database](https://static.googleusercontent.com/media/research.google.com/en//archive/spanner-osdi2012.pdf)

###### James C. Corbett, Jeffrey Dean, Michael Epstein

---

### What is the Problem? [Good papers generally solve *a single* problem]

Solutions that replicate data across datacenters as a storage service have either high communication costs rendering them unscalable or have minimal support for external consistency

### Summary [Up to 3 sentences]

Spanner distributes data at a global scale and support externally-consistent distributed transactions. Applications can specify constraints to control data read/write latency and it also provides externally consistent reads/writes and globally-consistent reads across the database at a timestamp.

### Key Insights [Up to 2 insights]

- TrueTime is implemented by a set of time master machines per datacenter and a timeslave daemon per machine. Daemons apply Marzullo’s algorithm to detect and reject liars,
and synchronize the local machine clocks to the nonliars.
- Spanner’s timestamp semantics (maintains a logical history log of all changes and written into Spanner for all transactions) made it efficient for Google's advertising backend (F1) to maintain in-memory data structures computed from the database state. F1 takes full snapshots of data at a timestamp to initialize data structures, and then reads incremental changes to update them. TrueTime enables Spanner to support atomic schema changes whereas it is infeasible to use a standard transaction, because number of groups in a database is scaled to the millions.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- The monotonicity invariant (Spanner assigns timestamps to Paxos writes in monotonically increasing order) allows Spanner to correctly determine whether a replica’s state is up-to-date enough to satisfy a read Transaction.
- Concurrent correctness properties guarantees that a whole-database audit read at a timestamp t will see exactly the effects of every transaction that has committed as of t

### Limitations/Weaknesses [up to 2 weaknesses]

- Client-application processes between datacenters have also to be moved in an automated, coordinated fashion in order for move data automatically in response to changing load on the client side.
- Data structure of local Nodes have relatively poor performance on complex SQL queries, because they were designed for simple key-value accesses.

### Summary of Key Results [Up to 3 results]

- Results show that is epsilon truly a bound on clock uncertainty. Sampling right after polling elides the sawtooth in epsilon due to local-clock uncertainty, and therefore measures time-master uncertainty that is generally 0.
- Considering increasing the number of replicas, latency still stays almost constant because Paxos executes in parallel at a group’s replicas and the latency to achieve a quorum becomes less sensitive to delay at one slave replica

### Open Questions [Where to go from here?]
- Shorter lease times would reduce the effect of server deaths on availability, but would require greater amounts of lease-renewal network traffic. Is there a mechanism that allows slaves to release their Paxos lease upon leader failure?
