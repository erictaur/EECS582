# [END-TO-END ARGUMENTS IN SYSTEM DESIGN](http://web.mit.edu/Saltzer/www/publications/endtoend/endtoend.pdf)

###### J.H. Saltzer, D.P. Reed and D.D. Clark

---

### What is the Problem? [Good papers generally solve *a single* problem]

This paper attempts to provide a provides a rationale for moving function upward in a layered system (the application level) since function placement has been a critical issue for a long time with without much conviction.

### Summary [Up to 3 sentences]

The author utilizes many parts of the data communication system to justify the reasoning of the implementation of end-to-end arguments. Which then extends to the range of other functions that can also fit the same argument.

### Key Insights [Up to 2 insights]

- [To-Be paraphrased] Clearly,  some  effort  at  the  lower  levels  to  improve  network  reliability  can  have  asignificant effect on application performance. But the key idea here is that the lower levels neednot provide "perfect" reliability.
- [To-Be paraphrased] Thus  the  end-to-end  argument  is  not  anabsolute rule, but rather a guideline that helps in application and protocol design analysis

### Notable Design Details/Strengths [Up to 2 details/strengths]

- Awareness of end-to-end arguments suppresses the urge of taking on more function than necessary.
- end-to-end arguments helps organize layering (assigning functions to different layers) is key to most layered communication protocols.

### Limitations/Weaknesses [up to 2 weaknesses]

- The Mystery Machine could recompute model changes incrementally rather than from scratch to account for the changes in the request model.
- The Mystery Machine makes the assumption that the segments in a call graph are acyclic. It is unclear how the system design would need to be changed in the presence of cycles (e.g., what happens when the same <event, task> pair appear more than once in a request trace).

### Summary of Key Results [Up to 3 results]

- There is significant variation in the contribution of major end-to-end performance components (servers, network, and client) to the critical path. One can use this variation to provide differentiated service (e.g., prioritizing service where the server has no slack, whereas deprioritizing those where network and client latency will likely dominate).
- Slack tends to remain stable for a given user across multiple Facebook sessions, so past slack information can be used to predict the slack of the current connection.

### Open Questions [Where to go from here?]

- The performance properties analyzed by the Mystery machine are fairly high-level. One interesting direction would be to extend this work to gather more information in a targeted way to do more low-level performance debugging (e.g., what code is responsible for the slow down?).
- The scope of the work can be extended to look into end-to-end performance analysis for mobile platforms in addition to the desktop.
