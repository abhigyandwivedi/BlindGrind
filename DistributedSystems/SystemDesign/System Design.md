# System Design and Architecture Resources

## Core Concepts

1. **Scalability**: [Link](https://lnkd.in/gpge_z76)
2. **Latency vs Throughput**: [Link](https://lnkd.in/g_amhAtN)
3. **CAP Theorem**: [Link](https://lnkd.in/g3hmVamx)
4. **ACID Transactions**: [Link](https://lnkd.in/gMe2JqaF)
5. **Rate Limiting**: [Link](https://lnkd.in/gWsTDR3m)
6. **API Design**: [Link](https://lnkd.in/ghYzrr8q)
7. **Strong vs Eventual Consistency**: [Link](https://lnkd.in/gJ-uXQXZ)
8. **Distributed Tracing**: [Link](https://lnkd.in/d6r5RdXG)
9. **Synchronous vs Asynchronous Communication**: [Link](https://lnkd.in/gC3F2nvr)
10. **Batch Processing vs Stream Processing**: [Link](https://lnkd.in/g4_MzM4s)

## Databases & Scaling

1. **Databases**: [Link](https://lnkd.in/gti8gjpz)
2. **Horizontal vs Vertical Scaling**: [Link](https://lnkd.in/gAH2e9du)
3. **Caching**: [Link](https://lnkd.in/gC9piQbJ)
4. **Distributed Caching**: [Link](https://lnkd.in/g7WKydNg)
5. **Load Balancing**: [Link](https://lnkd.in/gQaa8sXK)
6. **SQL vs NoSQL**: [Link](https://lnkd.in/g3WC_yxn)
7. **Database Scaling**: [Link](https://lnkd.in/gAXpSyWQ)
8. **Data Replication**: [Link](https://lnkd.in/gVAJxTpS)
9. **Data Redundancy**: [Link](https://lnkd.in/gNN7TF7n)
10. **Database Sharding**: [Link](https://lnkd.in/gMqqc6x9)
11. **Database Indexing**: [Link](https://lnkd.in/gCeshYVt)

## APIs and Communication

12. **WebSockets**: [Link](https://lnkd.in/g76Gv2KQ)
13. **API Gateway**: [Link](https://lnkd.in/gnsJGJaM)
14. **Message Queues**: [Link](https://lnkd.in/gTzY6uk8)

---

## Design Patterns
**Distributed Systems Patterns**

Clock-Bound Wait: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Wait to cover the uncertainty in time across cluster nodes before reading and writing values so that values can be correctly ordered across cluster nodes.

Consistent Core: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Maintain a smaller cluster providing stronger consistency to allow the large data cluster to coordinate server activities without implementing quorum-based algorithms.

Emergent Leader: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Order cluster nodes based on their age within the cluster to allow nodes to select a leader without running an explicit election.

Fixed Partitions: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Keep the number of partitions fixed to keep the mapping of data to partition unchanged when the size of a cluster changes.

Follower Reads: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Serve read requests from followers to achieve better throughput and lower latency.

Generation Clock: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): A monotonically increasing number indicating the generation of the server.

Gossip Dissemination: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Use a random selection of nodes to pass on information to ensure it reaches all the nodes in the cluster without flooding the network.

Heartbeat: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Show a server is available by periodically sending a message to all the other servers.

High-Water Mark: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): An index in the write-ahead log showing the last successful replication.

Hybrid Clock: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Use a combination of system timestamp and logical timestamp to have versions as date and time, which can be ordered.

Idempotent Receiver: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Identify requests from clients uniquely so you can ignore duplicate requests when a client retries.

Key-Range Partitions: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Partition data in sorted key ranges to efficiently handle range queries.

Lamport Clock: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Use logical timestamps as a version for a value to allow ordering of values across servers.

Leader and Followers: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Have a single server to coordinate replication across a set of servers.

Lease: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Use time-bound leases for cluster nodes to coordinate their activities.

Low-Water Mark: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): An index in the write-ahead log showing which portion of the log can be discarded.

Majority Quorum: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Avoid two groups of servers making independent decisions by requiring a majority for taking every decision.

Paxos: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Use two consensus-building phases to reach safe consensus even when nodes disconnect.

Replicated Log: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Keep the state of multiple nodes synchronized by using a write-ahead log that is replicated to all the cluster nodes.

Request Batch: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Combine multiple requests to optimally utilize the network.

Request Pipeline: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Improve latency by sending multiple requests on the connection without waiting for the response of the previous requests.

Request Waiting List: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Track client requests which require responses after the criteria to respond is met based on responses from other cluster nodes.

Segmented Log: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Split log into multiple smaller files instead of a single large file for easier operations.

Single-Socket Channel: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Maintain the order of the requests sent to a server by using a single TCP connection.

Singular Update Queue: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Use a single thread to process requests asynchronously to maintain order without blocking the caller.

State Watch: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Notify clients when specific values change on the server.

Two-Phase Commit: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Update resources on multiple nodes in one atomic operation.

Version Vector: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Maintain a list of counters, one per cluster node, to detect concurrent updates.

Versioned Value: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Store every update to a value with a new version, to allow reading historical values.

Write-Ahead Log: [Link](https://chatgpt.com/c/67a66b39-f6b0-8013-a3fd-c6126cd3237e#): Provide durability guarantee without requiring the storage data structures to be flushed to disk, by persisting every state change as a command to the append-only log.

---

## Architecture Patterns

45. **Event-Driven Architecture**: [Link](https://lnkd.in/dp8CPvey)
46. **Client-Server Architecture**: [Link](https://lnkd.in/dAARQYzq)
47. **Serverless Architecture**: [Link](https://lnkd.in/gQNAXKkb)
48. **Microservices Architecture**: [Link](https://lnkd.in/gFXUrz_T)

---

## Additional Resources

If you’re currently preparing for **DSA, HLD, and LLD**, check out my **one-stop resource guide on Topmate**:  
➡ [Link](https://lnkd.in/eYHSjbys) (400+ students are already using it!)

This guide will help you with:

- **DSA, HLD, and LLD for interviews**
- **Good resources that I used personally**
- **Lots of problems and case studies for DSA and system design**

---

_P.S: Note that I haven't created these resources, only curated them. Rights belong to respective parties._