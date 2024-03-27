
- Improve the performance of search queries.
- Decrease the write performance. This performance degradation applies to all insert, update, and delete operations.


---

### Index

An index in a database is a data structure that improves the speed of data retrieval operations on a database table. It works similarly to an index in a book, where you have a reference to the pages where a certain word or topic can be found.

Indexes are used to quickly locate data without having to search every row in a database table every time a database table is accessed. They can be created using one or more columns of a database table, providing the basis for both rapid random lookups and efficient access of ordered records.

The downside of indexes is that they need to be maintained, which can impact performance when performing operations like insertions, deletions, and updates that modify the indexed data. Therefore, it's important to find a balance and only use indexes when necessary.

In SQL, you can create an index using the `CREATE INDEX` statement, and remove it with the `DROP INDEX` statement. Here's an example of creating an index on a `customer_id` column in a `Orders` table:

```sql
CREATE INDEX idx_orders_customer_id
ON Orders (customer_id);
```

This would speed up queries that involve the `customer_id` column, such as `SELECT * FROM Orders WHERE customer_id = 123;`


---
Indexes in databases come with several advantages and disadvantages:

**Advantages**:

1. **Faster Data Retrieval**: The primary advantage of indexing is faster data retrieval. Indexes allow the database management system to find and retrieve specific rows much faster than it could do without an index.

2. **Order By Optimization**: Indexes can greatly speed up the `ORDER BY` clause, as the data is already sorted.

3. **Allows More Efficient Use of I/O**: By reducing the amount of data that needs to be read from disk, indexes can reduce the I/O operations.

**Disadvantages**:

1. **Space Requirement**: Every index requires additional disk space. If a database has a lot of indexes, this can significantly increase storage requirements.

2. **Overhead of Update Operations**: When a table is modified (INSERT, UPDATE, DELETE), the indexes on the table need to be updated as well. This can lead to slower write performance.

3. **Complexity**: Indexes add a level of complexity to the database schema and require careful design and management.

4. **May Not Be Beneficial for Small Tables**: For small tables, it might be faster to perform a full table scan rather than going through the overhead of using an index.

In summary, while indexes can greatly improve read performance, they come with trade-offs in terms of write performance, storage space, and complexity. Therefore, it's important to use them judiciously and monitor their impact on your database's performance.

---

#### DS for index

In databases, indexes are typically implemented using one of the following internal data structures:

1. **B-Tree**: The most common structure used for database indexing. B-Trees are tree data structures that keep data sorted and allow for efficient insertion, deletion, and search operations. The "B" stands for "balanced" because the tree remains balanced, meaning the leaf nodes are all at the same depth.

2. **Hash**: Hash indexes are used when you only want to retrieve data based on exact match conditions. They are extremely fast for these types of lookups but are not efficient for range queries or sorting operations.

3. **Bitmap**: Bitmap indexes use bit arrays (commonly known as bitmaps) and answer queries by performing bitwise logical operations on these bitmaps. They are most effective in databases with a large number of rows and a relatively small number of distinct values, making them ideal for data warehousing situations.

4. **R-Tree**: R-Trees are tree data structures used for spatial access methods, i.e., for indexing multi-dimensional information such as geographical coordinates, rectangles or polygons.

5. **Trie (Prefix Tree)**: Tries are used for indexing data that can be represented as a string. They are particularly effective for auto-complete functionality or IP routing.

The choice of which data structure to use for an index depends on the specific requirements of the database system and the nature of the data being stored.


---
