
- [CAP Theorem](https://en.wikipedia.org/wiki/CAP_theorem)
- Consistency: every read receives the most recent write or an error.
- Availability: every request receives a response that is not an error.
- Partition tolerance: the system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes
- CAP theorem implies that in the presence of a network partition, one has to choose between consistency and availability
- CAP is frequently misunderstood as if one has to choose to abandon one of the three guarantees at all times. In fact, the choice is really between consistency and availability only when a network partition or failure happens; at all other times, no trade-off has to be made.
- [ACID](https://en.wikipedia.org/wiki/ACID) databases choose consistency over availability.
- [BASE](https://en.wikipedia.org/wiki/Eventual_consistency) systems choose availability over consistency.


---
CAP Theorem is a concept in distributed data store systems that states it's impossible for a distributed system to simultaneously provide all three of the following guarantees:

1. **Consistency**: Every read receives the most recent write or an error. In other words, all nodes see the same data at the same time. It's as if the system behaves like a single entity, despite the fact that it's distributed.

2. **Availability**: Every request receives a (non-error) response, without the guarantee that it contains the most recent write. The system remains operational and can process requests even if part of the system is down or some of the data isn't up to date.

3. **Partition Tolerance**: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes. In other words, the system can sustain network failures that separate the system into isolated groups of nodes.

According to the CAP Theorem, a distributed system can only guarantee two out of these three properties at any given time. This means that system designers must make trade-offs depending on their specific use cases:

- **CP (Consistency/Partition Tolerance)**: These systems prioritize consistency and partition tolerance over availability. If a partition occurs, some nodes might not be able to provide responses to requests, but the ones that can will provide a consistent view of the data. An example of a CP system is HBase.

- **AP (Availability/Partition Tolerance)**: These systems prioritize availability and partition tolerance over consistency. All nodes can always provide a response, but it might not be the most recent data. Over time, as partitions are resolved, the data becomes consistent across nodes. An example of an AP system is DynamoDB.

- **CA (Consistency/Availability)**: These systems prioritize consistency and availability over partition tolerance. They are typically used in environments where network partitions are unlikely or rare, such as single data centers. However, in a real-world distributed system, network partitions can and do occur, so CA systems are less common. An example of a CA system is a traditional RDBMS like MySQL or PostgreSQL.

It's important to note that the CAP Theorem is a simplification, and real-world systems often make more nuanced trade-offs. For example, some systems might provide consistency and availability most of the time, but degrade to providing only one of them during network partitions.


---
ACID and BASE are two consistency models used in the field of computer science, particularly in the context of distributed systems and databases.

**ACID (Atomicity, Consistency, Isolation, Durability)**: 

ACID is a set of properties that guarantee that database transactions are processed reliably. 

- **Atomicity**: Ensures that all operations within a work unit are completed successfully; otherwise, the transaction is aborted at the point of failure, and all the previous operations are rolled back to their former state.
- **Consistency**: Ensures that the database properly changes states upon a successfully committed transaction.
- **Isolation**: Enables transactions to operate independently of and transparent to each other.
- **Durability**: Ensures that the result or effect of a committed transaction persists in case of a system failure.

ACID properties are strongly consistent, making them a good fit for applications where consistency is critical, such as banking systems.

**BASE (Basically Available, Soft state, Eventual consistency)**:

BASE is a consistency model used in distributed systems which prioritizes availability over consistency.

- **Basically Available**: This guarantees the availability of the data as regards CAP Theorem but it does not guarantee that the data will be the most recent or up-to-date. 
- **Soft State**: The state of the system could change over time, even without input due to the eventual consistency model.
- **Eventual Consistency**: This ensures that the system will become consistent over time, given that the system doesn't receive input during that time.

BASE properties provide high availability and are designed to handle failure gracefully. They are a good fit for systems where data is distributed and where it's acceptable for clients to have a slightly out-of-date view of the data, such as social media platforms.