
## Common types of NoSQL
### Key-value stores
- Array of key-value pairs. The "key" is an attribute name.
- Redis, Vodemort, Dynamo.

### Document databases
- Data is stored in documents.
- Documents are grouped in collections.
- Each document can have an entirely different structure.
- CouchDB, MongoDB.

### Wide-column / columnar databases
- Column families - containers for rows.
- No need to know all the columns up front.
- Each row can have different number of columns.
- Cassandra, HBase.

### Graph database
- Data is stored in graph structures
  - Nodes: entities
  - Properties: information about the entities
  - Lines: connections between the entities
- Neo4J, InfiniteGraph

## Differences between SQL and NoSQL
### Storage
- SQL: store data in tables.
- NoSQL: have different data storage models.

### Schema
- SQL
  - Each record conforms to a fixed schema.
  - Schema can be altered, but it requires modifying the whole database.
- NoSQL:
  - Schemas are dynamic.

### Querying
- SQL
  - Use SQL (structured query language) for defining and manipulating the data.
- NoSQL
  - Queries are focused on a collection of documents.
  - UnQL (unstructured query language).
  - Different databases have different syntax.

### Scalability
- SQL
  - Vertically scalable (by increasing the horsepower: memory, CPU, etc) and expensive.
  - Horizontally scalable (across multiple servers); but it can be challenging and time-consuming.
- NoSQL
  - Horizontablly scalable (by adding more servers) and cheap.

### ACID
- Atomicity, consistency, isolation, durability
- SQL
  - ACID compliant
  - Data reliability
  - Gurantee of transactions
- NoSQL
  - Most sacrifice ACID compliance for performance and scalability.

## Which one to use?
### SQL
- Ensure ACID compliance.
  - Reduce anomalies.
  - Protect database integrity.
- Data is structured and unchanging.

### NoSQL
- Data has little or no structure.
- Make the most of cloud computing and storage.
  - Cloud-based storage requires data to be easily spread across multiple servers to scale up.
- Rapid development.
  - Frequent updates to the data structure.
---

A NoSQL database is a type of database that provides a mechanism for storage and retrieval of data that is modeled in means other than the tabular relations used in relational databases (SQL databases). NoSQL databases are often used in big data and real-time web applications.

**Why do we need NoSQL databases?**

1. **Scalability**: NoSQL databases are designed to expand easily to accommodate data growth.
2. **Big Data**: They are well-suited for working with large sets of distributed data.
3. **Flexibility**: NoSQL databases allow for flexible schema design, which can be altered as needs change.
4. **Performance**: They are optimized for specific types of queries and can outperform SQL databases for certain workloads.

**Types of NoSQL databases:**

1. **Document databases** pair each key with a complex data structure known as a document. Documents can contain many different key-value pairs, or key-array pairs, or even nested documents. Example: MongoDB.
2. **Graph stores** are used to store information about networks of data, such as social connections. Example: Neo4J.
3. **Key-value stores** are the simplest NoSQL databases. Every single item in the database is stored as an attribute name (or 'key'), together with its value. Examples: Redis, DynamoDB.
4. **Wide-column stores** such as Cassandra and HBase are optimized for queries over large datasets, and store columns of data together, instead of rows.

**When to use which type?**

1. **Document databases** are a good choice when you have a variety of data types and need a flexible schema that can evolve over time.
2. **Graph databases** are ideal for dealing with interconnected data and complex queries.
3. **Key-value stores** are excellent for scenarios where you need to store large amounts of data but you don't need to perform complex queries to retrieve it.
4. **Wide-column stores** are a good choice when you need to store and query large amounts of data.

**Advantages of NoSQL databases:**

1. **Scalability**: NoSQL databases are designed to be scaled out across many servers.
2. **Performance**: They can outperform relational databases for certain types of workloads.
3. **Flexibility**: They allow for flexible schema design.

**Disadvantages of NoSQL databases:**

1. **Maturity**: SQL databases have been around for a long time and have a huge amount of tooling and resources available.
2. **Transactions**: NoSQL databases often don't provide the same level of transactional consistency as SQL databases.
3. **Querying**: Querying NoSQL can be more complex, particularly for those used to SQL.

**Difference between NoSQL and SQL databases:**

1. **Schema**: SQL databases require that you use a predefined schema for your data. NoSQL databases allow you to store data with an ad hoc schema.
2. **Scalability**: SQL databases are typically scaled by upgrading the hardware on a single server (vertical scaling). NoSQL databases are designed to scale across many servers (horizontal scaling).
3. **Transactions**: SQL databases typically provide ACID (Atomicity, Consistency, Isolation, Durability) properties. NoSQL databases often do not.
4. **Normalization**: SQL databases encourage data normalization. NoSQL databases often allow for, and encourage, data denormalization.
5. **Query Language**: SQL databases use SQL for defining and manipulating the data. In NoSQL database, queries are focused on a collection of documents, sometimes the database includes its own query language (like MongoDB), or only provides a simple API for data manipulation.


---

#### ACID

ACID is an acronym that stands for Atomicity, Consistency, Isolation, and Durability. These are a set of properties that guarantee that database transactions are processed reliably.

1. **Atomicity**: This property ensures that a transaction is treated as a single, indivisible unit of work. That means either all the changes made in a transaction are committed to the database, or if the transaction fails, none of the changes are committed. There's no such thing as a partial transaction. If a transaction is interrupted (for example, by a power outage), any changes it made are rolled back, and the database remains unchanged.

2. **Consistency**: This property ensures that a transaction brings the database from one valid state to another. The database has a set of integrity constraints (like unique key constraints), and all transactions should leave the database in a state where these constraints are satisfied. If a transaction would violate these constraints, it is rolled back and no changes are made.

3. **Isolation**: This property ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially. This means that the execution of one transaction is not affected by the execution of other transactions. If two transactions are executed concurrently, the changes made by one transaction are not visible to the other until the first transaction is committed.

4. **Durability**: This property ensures that once a transaction has been committed, it will remain committed even in the case of a system failure (like a power outage or crash). This is typically achieved by storing committed transactions in a transaction log that can be replayed to recreate the system state right before the failure. A system crash or restart does not affect the durability property.

These ACID properties are a key feature of SQL databases and are crucial for applications where data consistency is important, such as banking or airline reservation systems.


----


1. **Key-Value Databases**: These are the simplest type of NoSQL databases where each item is stored as a key paired with its value. The key is used to retrieve the value. They are highly optimized for retrieval and appending operations and offer high performance and can store schema-less data.

   **Example**: Redis, DynamoDB

   **Use Case**: Caching, Session Management, User Preferences, Serving Ad Content

   **Sample Structure**: 
   ```
   Key: "User123"
   Value: "{ 'Name': 'John', 'Age': 30, 'Email': 'john@example.com' }"
   ```

2. **Columnar Databases**: These databases store data by columns rather than by rows. They are designed to efficiently write and read data to and from hard disk storage in a block-oriented manner. They are best suited for analyzing large datasets, and they can quickly aggregate data across many rows.

   **Example**: Cassandra, HBase

   **Use Case**: Big Data Processing, Data Warehousing, Business Intelligence

   **Sample Structure**: 
   ```
   RowKey: "User123"
   ColumnFamily: "PersonalInfo"
   Column: "Name", Value: "John"
   Column: "Age", Value: "30"
   Column: "Email", Value: "john@example.com"
   ```

3. **Graph Databases**: These databases are designed to handle data whose relations are best represented as a graph and has elements which are interconnected, with an undetermined number of relations between them. They are perfect for storing data that has complex many-to-many relationships.

   **Example**: Neo4J, Amazon Neptune

   **Use Case**: Social Networks, Fraud Detection, Real-Time Recommendation Engines

   **Sample Structure**: 
   ```
   Node: "User", Properties: { 'Name': 'John', 'Age': 30 }
   Node: "Email", Properties: { 'Email': 'john@example.com' }
   Relationship: "HAS_EMAIL", Properties: { 'Verified': true }
   ```

4. **Document Databases**: These databases store data in documents similar to Key-Value, but they also add more complexity by offering nested data. This is a great option if you need to store unstructured or semi-structured data with varying schemas.

   **Example**: MongoDB, CouchDB

   **Use Case**: Content Management Systems, Catalogs, User Profiles

   **Sample Structure**: 
   ```
   {
     "_id": "User123",
     "Name": "John",
     "Age": 30,
     "Email": "john@example.com",
     "Address": {
       "Street": "123 Main St",
       "City": "Springfield",
       "State": "Unknown",
       "PostalCode": "12345"
     }
   }
   ```