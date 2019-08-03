---
title: Mining 
weight: 5
#pre: "<b>1. </b>"
# chapter: true
---

**Q:** Why choose Cuckoo Cycle POW?

**A**: Proof-of-Work(PoW) is used to confirm transactions and produces new blocks, therefore it is a very important engine in PoW cryptocurrencies. PoW must not enable a participant to have a significant advantage over another participant. That is why Satoshi said: "Proof-of-work is essentially one-CPU-one-vote." However, most widely used proof-of-work algorithms, such as SHA-256, Blake2b, Scrypt, are more efficient on ASIC devices when compared to CPUs and GPUs. This can lead to ASIC owners posses a much larger voting power than CPU and GPU owners. It violates the “one-CPU-one-vote” principle. 

Cuckoo-Cycle-PoW ,a graph-theoretic proof-of-work algorithm. It is ASIC resistant. This algorithm focuses more on memory use, meaning the solution time is bound to memory bandwidth rather than the raw processor or GPU speed. 

The Cuckoo-Cycle algorithm is designed to find certain subgraphs in large pseudo-random graphs. In particular, Search for cycles of specified length L in a bipartite graph with M edges of N nodes. If a cycle is found and the hash difficulty is less than the target difficulty, the cuckoo cycle PoW is completed.
