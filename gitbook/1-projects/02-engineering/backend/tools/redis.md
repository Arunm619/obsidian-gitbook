
Redis is an **open-sourced in-memory data structure store.**
that can be used 
1. Database
2. Cache
3. Message Broker
4. Streaming engine

Some data structures that Redis provides

1. Hash
2. List
3. Set
4. Sorted Set
5. Bitmap
6. Hyperloglog
7. Geospatial Indexes
8. Streams

These data structures can be used to build a variety of applications 

- Real time chat
- Auth Session Store
- Message Buffers
- Media Streaming
- Gaming Leaderboards
- Realtime analytics

Redis interest is off the charts as it has seen a wide range of applications across the industry. 

Flexibility and Simplicity. 

---
# What makes Redis Special?

Every Operation On Redis is **Atomic**

- Putting a key
- Adding to the list
- Set Union | intersection
- Incrementing the value 

When a command is executing, Redis doesn't context switch and start executing other command. It takes time to complete that operation and only then it picks up the other command. Hence its called atomic.

Beauty of Redis - Authoritative stamp - atomic in nature - no need to worry about concurrency at all - Everything is atomic in nature - no context.

Even `count++` is not thread safe. But here everything is atomic. 

---

### In Memory Data Store

Data is stored in memory. Hence the most common use of redis is cache.
But Redis also provides configurable persistence.
- Periodically dump data to disk
	- This is to act as a restore check point when something goes wrong. It doesn't have to start from scratch rather load the last checkpoint and get back to action.
- Write Ahead Log of all commands 
	- Every update command that is fired is logged to Append Only File (AOF) 
	- Redis logs every command into that so that it can reconstruct when something goes bad or setup asynchronous replication to another redis server
- No Persistence at all 
	- Ok losing all the data, just live in the memory.

---
# Other Key Features

- Transactions 
	- When one transaction is executing, nothing else would do. Roll backs.
- Pub/Sub on a topic
	- Publisher and Lot of Consumers listening on a particular topic. Push based message.
- TTL on Keys
	- Expiration on the keys after a set time.
	- Avoid Memory leaks by not storing things permanently
	- User authentication for 30 mins
	- For anything Temporary, this is the way to go,
- LRU Eviction
	- Key Eviction Strategy
	- Will not say its full, but it will remove the existing key based on a strategy. 


----
# Concurrent Programming Model (Single Process)

How to achieve concurrency in a single process mode. 
Redis working in a single process how does it handle multiple requests concurrently?


Concurrent programming is all about doing more than one thing at the same time.

#### MultiThreading

Each incoming request over the network is accepted by the server and executed in a separate thread. 

Eg.

Request 1 -> k ++  (Increment K) -> Thread 1
Request 2 -> k ++ (Increment K) -> Thread 2

**How to ensure data correctness?****

if `k = 10`, and two threads executing `k++` then possible final values are 11 and 12.

we have to make other threads wait while one thread is executing the critical section.

Hence we have `safeguard` 
1. Mutex 
2. Semaphores
These are pessimistic locking.

```algorithm
ACQUIRE LOCK
DO CRITICAL SECTION
RELEASE LOCK
```



----

