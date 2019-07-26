---
title: Block DAG 
weight: 5
#pre: "<b>1. </b>"
# chapter: true
---

**Q:** relationship between blockchain and blockDAG.

**A**: Through the evolving history from BlockChain to BlockDAG, it may indicate that BlockChain is a particular case of BlockDAG in the event of low throughput, which means both are the same in essence. As a result,  it is the scaling approach whose paradigm is the closest to the bitcoin network. BlockDAG is robust since it inherits all the long-time-proved stable features of bitcoin. Furthermore, it could scale infinitely in terms of protocol, unless it is limited physically, such as network bandwidth and propagation delay. A robust public chain is an optimal basis for incorporating further scaling solutions, such as sharding and state-channels; thus, BlockDAG is the preferred scaling solution of Qitmeer. 

**Q:** how does SPECTRE work with GHOSTDAG.

**A:**
SPECTRE works perfectly for the payment network. Its stateless voting consensus algorithms brings extreme fast confirmation time; in other words, users wait merely a few seconds to accept a transaction. However, the trade-off is that it does not support the total ordering of transactions that GhostDAG could offer, which will bring two problems.

Firstly, it would make double-spending transactions delayed indefinitely. This weakness will merely affect malicious users since only they have the capability. Nevertheless, Qitmeer hopes that the protocol is robust enough to make sure every case behaving consistently.  Therefore, once such incident happens, GhostDAG will solve the conflict by their global order.

Secondly, the rewards mechanism requires an ordered block list to prioritize mining rewards. Although GhostDAG rewarding confirmation is not as fast as SPECTRE, the mining rewards demands a long time maturity to spend, which is quite enough for GhostDAG to reach confirmation.

**Q:** Qitmeer innovation on BlockDAG.

**A:**
Qitmeer consensus protocol mainly originates from 3 BlockDAG papers published by DAGlabs - SPECTRE, GHOSTDAG and Inclusive. 

SPECTRE's matches the high liquidity demands of Qitmeer due to its fast confirmation, high throughput and bitcoin equivalent security. 
GHOSTDAG solves SPECTRE's weak liveness and provides total ordering service for rewards mechanism.

Qitmeer utilizes Inclusive to design its rewards mechanism, which has provided a weighted algorithm to balance the priority service in terms of transaction fee and transaction collision.

Qitmeer is grateful for DAGlabs work and has contributed power to DAGlabs community as a return. However, as we all believe, there is a long distance from research to implementation. 

First, integration has excellent value. Bitcoin's most significant innovation is that it has integrated various existing technologies rather than invented them. As far as we know by now, there are some proof-of-concept projects, even complete projects, implemented an individual protocol, but none of them has integrated all. As I just analyzed, the three papers are solving different problems and should work with each other as a whole system.

Second, optimization is critical to practice. The paper provides theory support for core problems but inevitably skips details.  For instance, the reference algorithms for SPECTRE and GHOSTDAG are intensive in computation, whereas Qitmeer has optimized both consensus algorithms by totally independent work. Moreover, the high throughput will bring high pressure on ledger storage, Qitmeer has proposed a compact storage solution to alleviate this problem. Also, Qitmeer will give a proposal on how to improve the bandwidth efficiency to increase scalability. 

**Q:** why choose SPECTRE as core consensus protocol

**A:**
SPECTRE is a secure BlockDAG protocol with fast confirmation and high throughput. GHOSTDAG  supports total ordering of transactions, which is the foundation of on-chain smart contract but sacrifices fast confirmation. So there is a trade-off between fast confirmation and on-chain smart contract. 

Qitmeer is dedicated to serving Islamic finance, which requires massive liquidity support, so high throughput and fast confirmation are the most top priority. Qitmeer never planned to implement on-chain smart contract because it is still too intensive in computation even though BlockDAG is scalable. We believe you still have an impression on the CryptoCat incident, which caused ethereum denial of service. Another consideration is that SPECTRE has a more straightforward design and two years maturity. We don't find any security risks feedback so far, so Qitmeer tends to trust it is desirably robust.