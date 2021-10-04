# [Imperfect Forward Secrecy: How Diffie-Hellman Fails in Practice](https://weakdh.org/imperfect-forward-secrecy-ccs15.pdf)

###### David Adrian, Karthikeyan Bhargavan, Zakir Durumeric

---

### What is the Problem? [Good papers generally solve *a single* problem]

The paper exposes a vulnerability of the Diffie-Hellman key exchange protocol which lets attackers to downgrade connections to export a weaker cipher suite.

### Summary [Up to 3 sentences]

The paper presented an approach enabled by this vulnerability that demonstrated a man-in-the-middle network attacker to downgrade a TLS connection to use 512-bit DH export-grade cryptography, allowing them to read the exchanged data and inject data into the connection. 

### Key Insights [Up to 2 insights]

- The authors performed NFS precomputations for the two most popular 512-bit primes (export-grade) on the web, so that quick computations of the discrete log for any key-exchange message are possible.
- The authors also implemented a man-in-the-middle network that sits between the TLS client and any DHE_EXPORT compliant server. The implementation overcame the challenge of compute the shared secret gab before the handshake completes in order to forge a Finished message.

### Notable Design Details/Strengths [Up to 2 details/strengths]

- The paper also discovered/unearthed other exploitable security loopholes in the DHE configurations.
- The author also brought up the idea of how NSA is defeating the VPN traffic encryption due to NSA's capability to crack 1024-bit Diffie-Hellman groups.

### Limitations/Weaknesses [up to 2 weaknesses]

- Elliptic curve discrete log algorithms do not gain as much of an advantage from precomputation, hence a transition to elliptic curves avoids logjam or other related cryptanalytic attacks.
- By disabling DHE_EXPORT on all servers, the premises of logjam collapses; since only attackers with national-level resources are capable of performing the required computation.

### Summary of Key Results [Up to 3 results]

- The problems of DH stem from the fact that the number field sieve for discrete log allows an attacker to perform precomputation that depends only on the group, after which computing individual logs in that group has a far lower cost.
- The basis that formed the attack stemmed from the fact that the signed portion of the server’s message fails to include any indication of the specific ciphersuite that the server has chosen. An attacker can rewrite the client’s request to offer a corresponding DHE_EXPORT ciphersuite accepted by the server and remove other ciphersuites that could be chosen instead.

### Open Questions [Where to go from here?]

- If administrators are responsible for generating unique/stronger Diffie-Hellman groups using safe primes for each website or server, isn't this putting the load of prime generation on the server side? Or is there a way to off-load the workload?
