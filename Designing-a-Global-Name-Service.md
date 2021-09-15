# [Designing a Global Name Service](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/acrobat-15.pdf)

###### Butler W. Lampson

---

### What is the Problem? [Good papers generally solve *a single* problem]

This paper gives a brief touch on a design of a name service, which maps a name to a set of properties. It is the basis for resource location.

### Summary [Up to 3 sentences]

The paper listed the requirements of a name service and listed design considerations at the client, administrative levels. Also the name space and update of values were also touched upon.

### Key Insights [Up to 2 insights]

- Clear emphasis on how the hierarchical system is constructed and how it operates: facilities for reading/updating a specific DI; access control and authentication.
- Clearly states that the name service is no file-system; the paper demonstrates how a name service should perform a given lookup extremely fast in a tree way larger than a file-system

### Notable Design Details/Strengths [Up to 2 details/strengths]

- The sweep is relatively easier to implement compared to allowing DC to send messages to one another and is also more reliable when considering the ring topology.
- The name space abstraction covers a lot of the design space for a name service; Particularly the growth and restructing seems really critical due to the huge directory the service will be dealing with eventually,

### Limitations/Weaknesses [up to 2 weaknesses]

- Why exactly is a hierarchical system required? It seems like reasonable to do so and that the author thinks its obvious, but he doesn't justify his statement.
- Specifications for the name interface is not really organized

### Summary of Key Results [Up to 3 results]

- At the client level: the name service provides the facilities for reading/updating values. At the administrative level: the name service maintains the copies and keeps them synchronized with sweeps.
- Other abstractions such as the name space, client caching and semantics for directory copying and updating values.

### Open Questions [Where to go from here?]

- Is it safe to assume that names ot properties of a node change slowly?
