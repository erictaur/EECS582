# [Dynamo: Amazon’s Highly Available Key-value Store](https://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf)

###### Michael Chow, David Meisner, Jason Flinn, Daniel Peek, Thomas F. Wenisch

---

### What is the Problem? [Good papers generally solve *a single* problem]

Coping with intermittent outages in an very-large-scaled infrastructure which is consistent of millions of components is Amazon's standard mode of operation; A good key-value storage system can fight with the issue of an always existing small but significant number of server and network components that might fail at any given point in time.

### Summary [Up to 3 sentences]

Dynamo is a highly available key-value storage system that some of Amazon’s core services use to provide an experience that does is not intermittent. Dynamo uses a combination of techniques to achieve scalability and availability: (1) Data is partitioned and replicated using consistent hashing, and (2) consistency is facilitated by object versioning. Dynamo is incrementally scalable and allows service owners to scale up/down based on their current load.

### Key Insights [Up to 2 insights]

- One essential key principle is that centralized control in the past has resulted in outages and the goal is to avoid it as much as possible. This leads to a simpler, more scalable, and more available system.
- In order to scale incrementally, Dynamo employs a mechanism to dynamically partition the data over the set of nodes in the system. Dynamo’s partitioning scheme relies on consistent hashing to distribute the load across multiple storage hosts.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- Dynamo uses a variant of consistent hashing instead of mapping a node to a single point, each node gets assigned to multiple points in the ring. Meaning that Dynamo uses the concept of virtual nodes, which looks like a single node in the system, but each node can be responsible for more than one virtual node. This solve the issues of the basic hashing algorithm which is oblivious to the heterogeneity in the performance of nodes.
- Vector clocks used in Dynamo capture causality between different versions of the same object and it determines whether two versions of an object have a causal ordering, by examine their vector clocks. If the counters on the first object’s clock are <= to all of the nodes in the second clock, then the first is an ancestor of the second and can be forgotten.

### Limitations/Weaknesses [up to 2 weaknesses]

- For applications other than Amazon that want to use Dynamo, analysis is required during the starting stages of the development to pick the right conflict resolution mechanisms that meet the business case appropriately.

### Summary of Key Results [Up to 3 results]

- Dynamo provides the necessary knobs using the N/R/W parameters to tune their instance based on their needs. A full membership model used by Dynamo where each node is aware of the data hosted by its peers. To do this, each node actively gossips the full routing table with other nodes in the system.
- The optimization of allowing writes to be coordinated accordingly to the preference list enables Dynamo to pick the node that has the data that was read by the preceding read operation. This increases the chances of achieveing consistency of read-your-writes. This also reduces variability in the performance of the request handling. 
- The strategy of dividing hash space into Q equally sized partitions and partition placement is decoupled from the partitioning scheme. This strategy allows for faster bootstrapping/recovery due to the fact that partition ranges are fixed so that they can be stored in separate files.
