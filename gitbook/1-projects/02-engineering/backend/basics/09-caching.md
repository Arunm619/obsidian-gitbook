
- Take advantage of the locality of reference principle: recently requested data is likely to be requested again.
- Exist at all levels in architecture, but often found at the level nearest to the front end.

## Application server cache
- Cache placed on a request layer node.
- When a request layer node is expanded to many nodes
  - Load balancer randomly distributes requests across the nodes.
  - The same request can go to different nodes.
  - Increase cache misses.
  - Solutions:
    - Global caches
    - Distributed caches

## Distributed cache
- Each request layer node owns part of the cached data.
- Entire cache is divided up using a consistent hashing function.
- Pro
  - Cache space can be increased easily by adding more nodes to the request pool.
- Con
  - A missing node leads to cache lost.

## Global cache
- A server or file store that is faster than original store, and accessible by all request layer nodes.
- Two common forms
  - Cache server handles cache miss.
    - Used by most applications.
  - Request nodes handle cache miss.
    - Have a large percentage of the hot data set in the cache.
    - An architecture where the files stored in the cache are static and shouldn’t be evicted.
    - The application logic understands the eviction strategy or hot spots better than the cache

## Content Delivery network (CDN)
- For sites serving large amounts of static media.
- Process
  - A request first asks the CDN for a piece of static media.
  - CDN serves that content if it has it locally available.
  - If content isn’t available, CDN will query back-end servers for the file, cache it locally and serve it to the requesting user.
- If the system is not large enough for CDN, it can be built like this:
  - Serving static media off a separate subdomain using lightweight HTTP server (e.g. Nginx).
  - Cutover the DNS from this subdomain to a CDN later.

## Cache invalidation
- Keep cache coherent with the source of truth. Invalidate cache when source of truth has changed.
- Write-through cache
  - Data is written into the cache and permanent storage at the same time.
  - Pro
    - Fast retrieval, complete data consistency, robust to system disruptions.
  - Con
    - Higher latency for write operations.
- Write-around cache
  - Data is written to permanent storage, not cache.
  - Pro
    - Reduce the cache that is no used.
  - Con
    - Query for recently written data creates a cache miss and higher latency.
- Write-back cache
  - Data is only written to cache.
  - Write to the permanent storage is done later on.
  - Pro
    - Low latency, high throughput for write-intensive applications.
  - Con
    - Risk of data loss in case of system disruptions.

## Cache eviction policies
- FIFO: first in first out
- LIFO: last in first out
- LRU: least recently used
- MRU: most recently used
- LFU: least frequently used
- RR: random replacement


---
Caching is a technique used in computing to store data in a temporary storage area, often called a cache, to retrieve it faster in subsequent requests. The data stored in a cache might be the result of an earlier computation or a copy of data stored elsewhere.

**Types of Caching:**

1. **Memory Cache:** This is the fastest type of caching. It stores data in the system's RAM, which is much faster to access than disk storage.

2. **Disk Cache:** This type of cache stores data on the disk. It's slower than memory cache but can store more data.

3. **Database Caching:** This type of cache is used to reduce the load on the database by storing the result of a query.

4. **Web Caching:** This type of cache is used to store web pages and other online content to reduce server load and improve website load times.

5. **Distributed Caching:** This type of cache is used in distributed systems where data is stored across multiple nodes.

**Advantages of Caching:**

1. **Improved Performance:** Caching can significantly improve the performance of a system by reducing the time it takes to access data.

2. **Reduced Network Costs:** By storing data closer to the user, caching can reduce the amount of data that needs to be sent over the network.

3. **Scalability:** Caching can help a system scale to handle more users by reducing the load on the system's backend.

**Disadvantages of Caching:**

1. **Stale Data:** One of the main disadvantages of caching is the possibility of serving stale data. If the original data changes and the cache isn't updated, the system might serve outdated data.

2. **Complexity:** Implementing caching can add complexity to a system. It requires careful management to ensure data consistency and integrity.

3. **Cost:** While caching can reduce network costs, it can also increase the cost of the system due to the need for additional storage.

In system architecture, caching is used to improve the performance and scalability of a system. For example, a web application might cache web pages to reduce the load on its servers and improve page load times for users. Similarly, a database might use caching to reduce the number of disk reads it needs to perform, improving query performance.



----
#### Locality principle

The principle of locality of reference, also known as the locality principle, is a concept that is widely used in caching. It refers to the tendency of a processor to access the same set of memory locations repetitively over a short period of time. This principle is the basis for the effectiveness of the cache memory in a computer system.  There are two main types of locality:  
- Temporal Locality: If a memory location is referenced, it is likely to be referenced again in the near future. This is why we keep recently accessed items in the cache.  
- Spatial Locality: If a memory location is referenced, memory locations with nearby addresses are likely to be referenced in the near future. This is why when a cache miss occurs, we don't just load the requested data into the cache, but also the data around it.  
In the context of system design, understanding and leveraging the principle of locality of reference can lead to significant performance improvements. For example, when designing a data-intensive application, you might choose to keep frequently accessed data in a cache to reduce expensive database or network operations. Similarly, in a web application, you might cache frequently accessed web pages to reduce server load and improve response times.


-----
How to calculate cache hit ratio?

**Cache Performance:** The performance of the cache is measured in terms of hit ratio. When CPU refers to memory and find the data or instruction within the Cache Memory, it is known as cache hit. If the desired data or instruction is not found in the cache memory and CPU refers to the main memory to find that data or instruction, it is known as a cache miss.

```
Hit + Miss  = Total CPU Reference
Hit Ratio(h) = Hit / (Hit+Miss) 
Miss Ratio = 1 - Hit Ratio(h)
Miss Ratio = Miss / (Hit+Miss)
```


----
#### Cache concepts

The main goal of caching is to increase data retrieval performance by reducing the need to access the underlying slower storage layer. This is achieved by storing data that is frequently accessed or expensive to fetch in a faster storage medium.  Here are some key concepts related to caching:  
- Cache Hit: When the requested data is found in the cache, it's a cache hit. The system can quickly return the data from the cache without having to retrieve it from the primary storage.  
- Cache Miss: When the requested data is not found in the cache, it's a cache miss. The system must fetch the data from the primary storage and store it in the cache for future access.  
- Cache Eviction Policy: This is a strategy to decide which items to remove from the cache when it's full. Common policies include Least Recently Used (LRU), First In First Out (FIFO), and Least Frequently Used (LFU).  
- Cache Coherency: This is a consistency mechanism to ensure that all copies of data in different cache locations show the same value. This is crucial in multi-processor systems.  
- Write Policy: This determines how the system handles a write operation. In a write-through cache, data is written to both the cache and the primary storage. In a write-back cache, data is written to the cache first and then to the primary storage when the cache block is replaced.

---
#### Application Server cache

Application server caching is a technique where data is stored in a temporary storage area on a request layer node. This can significantly improve the performance of your application by reducing the need to access the underlying slower storage layer. 

However, when a request layer node is expanded to many nodes, and a load balancer randomly distributes requests across these nodes, the same request can go to different nodes, leading to an increase in cache misses.  

To solve this problem, you can use either global caches or distributed caches.  

- Global Caches: All nodes use the same single cache space. This involves adding a server, or file store of some sort, faster than the original store and accessible by all nodes. When one node updates the cache, all the other nodes have access to the updated data.  
- Distributed Caches: In this case, the cache is divided up using a consistent hashing function, such that if a request node is looking for a certain piece of data, it can quickly know where to look within the distributed cache to check if the data is available. This reduces the chance of a cache miss.

---
## Distributed cache

- Each request layer node owns part of the cached data.
- Entire cache is divided up using a consistent hashing function.
- Pro
    - Cache space can be increased easily by adding more nodes to the request pool.
- Con
    - A missing node leads to cache lost.

----
#### Global cache 
two forms:

- **Cache Server Handles Cache Miss**:
	This is the most commonly used form of global caching. In this case, the cache server is responsible for handling cache misses. When a request node queries the cache and doesn't find the data it needs (a cache miss), the cache server will fetch the data from the primary storage, store it in the cache, and return it to the request node.  
- **Request Nodes Handle Cache Miss**:
	In this architecture, the request nodes themselves are responsible for handling cache misses. This is typically used in scenarios where a large percentage of the hot data set is in the cache, the files stored in the cache are static and shouldn't be evicted, or the application logic understands the eviction strategy or hot spots better than the cache.

---
#### CDN (Content Delivery Network)

- CDN stands for Content Delivery Network. 
- It's a network of servers distributed across various locations worldwide to deliver web content more efficiently to users. 
- CDNs work by caching content, such as **images, videos, CSS, and JavaScript files**, on multiple servers. 
- When a user requests content, the CDN serves it from the server closest to the user's location, reducing latency and improving load times. This is especially useful for websites with global audiences or heavy traffic spikes.
- From CloudFlare : A content delivery network (CDN) is a geographically distributed group of servers that caches content close to end users. A CDN allows for the quick transfer of assets needed for loading Internet content, including HTML pages, JavaScript files, stylesheets, images, and videos.

CDNs offer several benefits, including:

1. Improved website performance: By delivering content from servers closer to users, CDNs reduce latency and improve page load times, resulting in a better user experience.
    
2. Scalability: CDNs can handle high volumes of traffic without affecting website performance, making them ideal for websites experiencing rapid growth or sudden traffic spikes.
    
3. Enhanced reliability: With content distributed across multiple servers, CDNs provide redundancy and failover protection, ensuring continuous availability of website content even in the event of server failures or network issues.
    
4. Security: Some CDNs offer security features such as DDoS protection, web application firewalls, and SSL/TLS encryption, helping protect websites from cyber attacks and unauthorized access.
    
----

#### CDN GPT Explanation

- A Content Delivery Network (CDN) is a system of distributed servers that deliver pages and other web content to a user, based on the geographic locations of the user, the origin of the webpage and the content delivery server. 
- This service is effective in speeding the delivery of content of websites with high traffic and websites that have global reach. 
- The closer the CDN server is to the user geographically, the faster the content will be delivered to the user. 
- Process
	- when a request for static media is made, the CDN will first check if it has the content locally available. 
	- If it does, it serves that content; if it doesn't, it will query the back-end servers for the file, cache it locally, and then serve it to the requesting user.  
	- For systems that are not large enough to warrant a CDN, a common approach is to serve static media off a separate subdomain using a lightweight HTTP server like Nginx. 
	- This setup can be beneficial because it offloads the task of serving static files from your main server, allowing it to focus on dynamic content. 
	- Furthermore, it provides an easy path to switch to a CDN later by simply changing the DNS records of the subdomain to point to the CDN.

----
#### Cache Invalidation Strategy

- Keep cache coherent with the source of truth. Invalidate cache when source of truth has changed.
- Cache invalidation is a critical aspect of any caching strategy. 
- It determines when an item in the cache should be considered stale and therefore needs to be updated or removed. 

There are several common strategies for cache invalidation:  

- Time to Live (TTL): Each item in the cache is given a TTL when it's stored. Once the TTL expires, the item is considered stale and is removed from the cache. This strategy is simple and works well for data that changes infrequently.  

- Write-Through: In this strategy, changes to data are written to the cache and the backing store at the same time. This ensures that the cache always contains the most up-to-date data, but it can slow down write operations.  

- Write-Behind (Back): Changes are written to the cache first and then written to the backing store later. This can speed up write operations, but there's a risk of data loss if the system crashes before the changes are written to the backing store.  

- Invalidate: When data is changed, instead of updating the cache, the corresponding entry in the cache is removed or marked as invalid. The next time the data is requested, it will be fetched from the backing store and the cache will be updated. 

----
**Cache write strategies** 

![[cache-write-strategies.png]]

- Write Through: In a write-through policy, data is simultaneously written to the cache and the backing store. This ensures that the cache always contains the most recent data, but it can slow down write operations because every write operation must update both the cache and the backing store. This strategy is beneficial when read operations are more frequent than write operations.  

- Write Back (or Write Behind): In a write-back policy, data is initially written only to the cache. The write to the backing store is deferred until the cache blocks are replaced. This policy can speed up write operations because it only updates the cache, not the backing store. However, there's a risk of data loss if the system crashes before the changes are written to the backing store.  

- Write Around: In a write-around policy, data is written directly to the backing store, bypassing the cache entirely. This can be beneficial when writing large amounts of data that isn't likely to be read soon, as it prevents the cache from being filled up with data that won't be used. However, if the data is read soon after being written, this policy can result in slower read operations because the data must be fetched from the backing store.


----
#### Cache Eviction Policies

Cache eviction policies determine which items to remove from the cache when it becomes full. Here's a brief explanation of the policies you mentioned:  
- FIFO (First In First Out): This policy evicts the oldest entry first, i.e., the entry that was added to the cache earliest.  (Streaming app)
- LIFO (Last In First Out): This policy evicts the most recently added entry first.  (Stack app)
- LRU (Least Recently Used): This policy evicts the entry that was least recently used.  (Web Browser)
- MRU (Most Recently Used): This policy evicts the entry that was most recently used.  (Predictive text input system)
- LFU (Least Frequently Used): This policy evicts the entry that is least frequently used.  (Music steaming app)
- RR (Random Replacement): This policy randomly selects an entry for eviction. (No clear pattern app)


**Examples**
- FIFO (First In First Out): in a **streaming application**, you might want to cache the most recent data and discard the oldest data.  
- LIFO (Last In First Out): This policy could be used in applications where the most recent data is less likely to be accessed in the near future. For example, in a stack-like data structure or an application that processes data in a stack-like manner.  
- LRU (Least Recently Used): This policy is useful in scenarios where you're likely to access recently used data again. For example, **in a web browser**, pages that were recently visited are likely to be visited again, so they are kept in the cache.  
- MRU (Most Recently Used): This policy could be used in applications where the most recently used data is less likely to be used in the near future. For example, in a predictive text input system, the most recently used words are less likely to be used immediately again.  
- LFU (Least Frequently Used): This policy is useful in scenarios where some data is accessed frequently and should be kept in cache. For example, in a music streaming application, popular songs that are played frequently could be kept in cache.  
- RR (Random Replacement): This policy could be used when there's no significant difference in the cost of fetching any piece of data, or when there's no clear pattern in the data access. For example, in a system with uniform data access patterns, RR could be a simple and effective strategy.


---
