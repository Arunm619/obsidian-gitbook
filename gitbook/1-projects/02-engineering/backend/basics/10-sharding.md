
## Partitioning methods

Partitioning - divide into parts.

Partitioning (sharding) **breaks up the dataset into smaller subsets**. Each partition becomes its own small database. Partitioning spreads the data and query load across multiple machines. Typically, the database will assign multiple partitions to a node.


- Horizontal partitioning
	  - Range based sharding.
	  - Also known as data sharding
	  - Put different rows into different tables.
	  - Con
	    - If the value whose range is used for sharding isn’t chosen carefully, the partitioning scheme will lead to unbalanced servers.
- Vertical partitioning
	  - Divide data for a specific feature to their own server.
	  - Pro
	    - Straightforward to implement.
	    - Low impact on the application.
	  - Con
	    - To support growth of the application, a database may need further partitioning.
- Directory-based partitioning
	  - A lookup service that knows the partitioning scheme and abstracts it away from the database access code.
	  - Allow addition of db servers or change of partitioning schema without impacting application.
	  - Con
	    - Can be a single point of failure.

## Partitioning criteria
- Key or hash-based partitioning
  - Apply a hash function to some key attribute of the entry to get the partition number.
  - Problem
    - Adding new servers may require changing the hash function, which would need redistribution of data and downtime for the service.
    - Workaround: [consistent hashing](https://en.wikipedia.org/wiki/Consistent_hashing).
- List partitioning
  - Each partition is assigned a list of values.
- Round-robin partitioning
  - With `n` partitions, the `i` tuple is assigned to partition `i % n`.
- Composite partitioning
  - Combine any of above partitioning schemes to devise a new scheme.
  - Consistent hashing is a composite of hash and list partitioning.
    - Key -> reduced key space through hash -> list -> partition.

## Common problems of sharding
Most of the constraints are due to the fact that operations across multiple tables or multiple rows in the same table will no longer run on the same server.

- Joins and denormalization
  - Joins will not be performance efficient since data has to be compiled from multiple servers.
  - Workaround: denormalize the database so that queries can be performed from a single table. But this can lead to data inconsistency.
- Referential integrity
  - Difficult to enforce data integrity constraints (e.g. foreign keys).
  - Workaround
    - Referential integrity is enforced by application code.
    - Applications can run SQL jobs to clean up dangling references.
- Rebalancing
  - Necessity of rebalancing
    - Data distribution is not uniform.
    - A lot of load on one shard.
  - Create more db shards or rebalance existing shards changes partitioning scheme and requires data movement.
---

### What is Sharding?

- Sharding is a type of database partitioning that separates very large databases into smaller, faster, more easily managed parts called data shards. The word shard means a small part of a whole.  Sharding is used in databases to improve performance. 
- As databases grow in size, queries become slower. Sharding is a method to keep the data distributed across multiple databases, or even multiple machines, to keep the performance of the system at an optimal level.  


- Horizontal Partitioning: Sharding involves breaking up one's database into two or more smaller databases (called shards), each holding a part of the data. This is known as horizontal partitioning. For example, a database with customer data could be sharded on the customer's location, with separate shards for different regions.  

- Distributed Data: Each shard runs on a separate database server instance, spreading the load. The distribution can be on the same physical machine or spread over various machines.  

-  Shard Key: Each record in a sharded system must have a designated shard key. This key is used to determine which shard the record belongs to. The shard key should be chosen carefully, as an inappropriate choice can lead to uneven distribution of data, negating the benefits of sharding.  

- Independence: Each shard is independent of the others and can be operated on without affecting the others. This means that operations on one shard do not affect operations on another shard, which can significantly improve performance for large scale applications.  

- Scalability: Sharding can also improve the scalability of an application, as adding a new shard can increase the storage capacity of the database.  

However, sharding comes with its own set of complexities. It can make queries and database maintenance more complex. Also, if the shards need to communicate with each other, the network overhead can slow down the system. Therefore, it's important to consider these factors when deciding whether to use sharding.

----
#### Types of partitioning

- Horizontal Partitioning: Also known as data sharding, horizontal partitioning involves dividing a database into two or more separate databases. Each of these databases, or shards, holds its own distinct set of rows. For example, a database of customers could be horizontally partitioned based on the customers' geographic location, with separate shards for different regions. This type of partitioning can help improve performance and manageability when dealing with large amounts of data.  

- Vertical Partitioning: In vertical partitioning, the database is divided based on columns instead of rows. Each partition or shard will hold its own distinct set of columns. For example, a customer database could be vertically partitioned into two databases: one holding contact information (name, address, phone number) and another holding order history. This can be useful when certain data is accessed together more frequently, improving performance by reducing the amount of data that needs to be read from disk.  

- Lookup Service Partitioning: This is a method of partitioning where a lookup service is used to direct traffic to the correct database shard. The lookup service maintains a directory of the shards and knows which shard holds which piece of data. When a request comes in, the lookup service directs the request to the appropriate shard. This can be useful in distributed systems where data is spread across multiple servers or locations, as it abstracts the complexity of finding the correct shard from the client.

Each of these partitioning strategies has its own advantages and trade-offs, and the choice of which to use depends on the specific requirements and characteristics of the system.

---

**Types of partitioning**

- Key or Hash-Based Partitioning: This method involves applying a hash function to some key attribute of the entry to determine the partition number. This can distribute data evenly across the partitions, but it has a significant drawback: if you add or remove servers, you may need to change the hash function, which would require redistributing the data and cause downtime for the service. A common solution to this problem is consistent hashing, which creates a hash ring and assigns keys to the nearest server in the ring. This allows for servers to be added or removed with minimal data reassignment.  

- List Partitioning: In this method, each partition is assigned a list of values. When a new entry comes in, the system checks which partition's list the entry's key belongs to, and assigns it to that partition. This can be useful when the key space is not uniform and certain keys should be grouped together.  

- Round-Robin Partitioning: This is a simple method where the ith tuple is assigned to partition i % n, where n is the number of partitions. This ensures a uniform distribution of data, but does not take into account the nature of the data.  

- Composite Partitioning: This method involves combining any of the above partitioning schemes to devise a new scheme. For example, consistent hashing is a composite of hash and list partitioning. First, a hash function reduces the key space, then a list determines which partition the key belongs to.

---

#### Problems with Sharding

- **Joins and Denormalization:** When data is distributed across multiple servers, performing joins can be inefficient as data has to be compiled from multiple sources. One workaround is to denormalize the database so that queries can be performed from a single table. However, this can lead to data inconsistency.  

- **Referential Integrity**: Enforcing data integrity constraints, such as foreign keys, can be difficult with sharded databases. One solution is to enforce referential integrity at the application level. This means the application code is responsible for ensuring data consistency. Additionally, SQL jobs can be run periodically to clean up any dangling references.  

- **Rebalancing**: Over time, data distribution may become uneven, or one shard may experience a higher load. This necessitates rebalancing, which involves creating more database shards or rebalancing existing ones. However, this changes the partitioning scheme and requires moving data, which can be a complex and resource-intensive process. 

---
#### what is referential integrity in database

Referential integrity is a property of data which, when satisfied, requires every value of one attribute (column) of a relation (table) to exist as a value of another attribute in a different (or the same) relation.

For example, if we have two tables, `Orders` and `Customers`, and `Orders` has a `customer_id` column that is intended to refer to a customer in the `Customers` table, referential integrity would enforce that you can't have a `customer_id` in the `Orders` table that doesn't exist in the `Customers` table.

This is typically enforced with foreign keys. A foreign key is a column or a set of columns in one table that is used to "refer" to a row in another table. The table with the foreign key is called the referencing table or child table, and the table that is referred to by the foreign key is called the referenced table or parent table.

In the example above, `customer_id` in the `Orders` table would be a foreign key referencing the `Customers` table. If referential integrity is enforced, the database wouldn't allow you to add an order with a `customer_id` that doesn't exist in the `Customers` table, or delete a customer from the `Customers` table if there are orders in the `Orders` table that refer to it.

Referential integrity is crucial in relational database design to ensure the consistency of data across multiple tables.


----

#### What is normalisation?

Normalization in a database is the process of organizing data to minimize redundancy and avoid data anomalies. It involves decomposing a table into less redundant (and smaller) tables but without losing information; defining foreign keys in the old table referencing the primary keys in the new ones. The objective is to isolate data so that additions, deletions, and modifications of a field can be made in just one table and then propagated through the rest of the database via the defined foreign keys.

There are several normal forms in normalization, each with a specific set of rules. They are as follows:

1. **First Normal Form (1NF)**: Each table cell should contain a single value, and each record needs to be unique.

2. **Second Normal Form (2NF)**: If a table contains a composite primary key, each non-key column should be a fact about the entire composite key.

3. **Third Normal Form (3NF)**: Every non-key column must be a fact about the primary key.

4. **Boyce-Codd Normal Form (BCNF)**: For any dependency A → B, A should be a super key.

5. **Fourth Normal Form (4NF)**: A table should not contain two or more independent multi-valued facts about an entity.

6. **Fifth Normal Form (5NF)**: Also known as Project-Join Normal Form (PJNF), a table should not contain redundancies that can be eliminated by decomposing it into smaller tables and then joining them.

Normalization helps improve the clarity, efficiency, and scalability of the database, but it's not always the best approach for every situation. Sometimes, denormalization (the process of combining tables to improve read performance) might be more suitable, especially in the context of large-scale data analytics and business intelligence applications.

---
