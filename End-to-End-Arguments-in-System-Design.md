# [END-TO-END ARGUMENTS IN SYSTEM DESIGN](http://web.mit.edu/Saltzer/www/publications/endtoend/endtoend.pdf)

###### J.H. Saltzer, D.P. Reed and D.D. Clark

---

### What is the Problem? [Good papers generally solve *a single* problem]

This paper attempts to provide a provides a rationale for moving function upward in a layered system (the application level) since function placement has been a critical issue for a long time with without much conviction.

### Summary [Up to 3 sentences]

The author utilizes many parts of the data communication system to justify the reasoning of the implementation of end-to-end arguments. Which then extends to the range of other functions that can also fit the same argument. The author also mentioned the subtlety when identifying the endpoints for different applications.

### Key Insights [Up to 2 insights]

- Some  effort  at  the  lower  levels  to  improve  network  reliability  can  have  asignificant effect on application performance. But the key idea here is that the lower levels need not provide perfect reliability.
- The  end-to-end  argument  is  not  anabsolute rule, but rather a guideline that helps in application and protocol design analysis

### Notable Design Details/Strengths [Up to 2 details/strengths]

- Awareness of end-to-end arguments suppresses the urge of taking on more function than necessary.
- end-to-end arguments helps organize layering (assigning functions to different layers) is key to most layered communication protocols.

### Limitations/Weaknesses [up to 2 weaknesses]

- The end-to-end argument is no absolute rule, and solutions rely heavily on the application domain.
- The entire reasoning are pretty much inclined to the qualitative side of the spectrum due to the nature of the problem.

### Summary of Key Results [Up to 3 results]

- The author listed a lot of examples (duplicate message suppresion/FIFO message delivery) to demonstrate the necessity of moving the end-to-end checks to the application level while pointing out the trade-offs for various placement of the end-to-end checks.
- The author also provided two similar examples with different properties (Accuracy versus latency concerns) to illustrate that one must use some care to identify the end points to which the end-to-end argument should be applied

### Open Questions [Where to go from here?]

- The implications analyzed by the author are fairly high-level and qualitative instead of quantitative. One could extend this work by benchmarking the different setups that placed the end-to-end checks at various levels.
