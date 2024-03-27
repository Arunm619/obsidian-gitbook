
Help scale horizontally across an ever-increasing number of servers.

LB locations
- Between user and web server
- Between web servers and an internal platform layer (application servers, cache servers)
- Between internal platform layer and database

## Algorithms

- Least connection
- Least response time
- Least bandwidth
- Round robin
- Weighted round robin
- IP hash

## Implementation

- Smart clients
- Hardware load balancers
- Software load balancers



---

Forward proxy Vs Reverse Proxy 

Forward proxy - VPN in mobile phones , masking client 
Reverse Proxy - Load balancer that masks the web/app servers.

----

Load balancing is a technique used to distribute network traffic across multiple servers. This ensures no single server bears too much demand, thereby improving responsiveness and availability of applications, websites, or databases. Load balancing is crucial for high-traffic, reliability-critical applications.

Here are some key concepts related to load balancing:

1. **Load Balancer**: This is a device that acts as a reverse proxy and distributes network or application traffic across a number of servers. Load balancers are used to increase capacity (concurrent users) and reliability of applications.

2. **Scheduling Algorithms**: Load balancers use various scheduling algorithms to determine which server to send requests to. Some common ones include Round Robin, Least Connections, and IP Hash.

    - **Round Robin**: Requests are distributed across the group of servers sequentially.
    - **Least Connections**: A new request is sent to the server with the fewest current connections to clients. This is quite useful when there are a significant amount of persistent connections in the traffic.
    - **IP Hash**: The IP address of the client is used to determine which server receives the request.

3. **Session Persistence**: Sometimes it's essential to route the client to the same server where they started the session for the sake of consistency (due to session data stored locally on the server). This is known as session persistence.

4. **Health Checks**: Load balancers also perform health checks on the servers in the pool to ensure they are responsive. If a server fails a health check, it is automatically removed from the pool, and traffic is directed to other servers.

5. **Layer 4 and Layer 7 Load Balancing**: Load balancing can occur either at Layer 4 (transport layer, e.g., TCP) or Layer 7 (application layer, e.g., HTTP) of the OSI model. Layer 7 load balancing allows for more sophisticated traffic distribution decisions based on attributes such as HTTP header, cookies, or data type.

In the context of web applications, load balancing can be implemented using various technologies including hardware load balancers, software-based load balancers, or even cloud-based load balancers provided by cloud service providers like AWS, Google Cloud, or Azure.


-----
Sure, let's dive deeper into these load balancing algorithms:

1. **Round Robin**: This is the simplest method of load balancing. In this method, the load balancer forwards a client request to each server in turn. When it reaches the end of the list, it starts again from the top. For example, if you have three servers A, B, and C, the first request goes to A, the second to B, the third to C, the fourth back to A, and so on. This method doesn't consider the current load of each server, so it works best when the servers are of equal specification and the tasks are of equal load.

2. **Least Connections**: In this method, the load balancer keeps track of how many connections each server is handling. It forwards new requests to the server with the fewest active connections. This method is more dynamic than Round Robin as it considers the load of each server. For example, if server A is handling 2 connections, server B is handling 3 connections, and server C is handling 1 connection, the next request will go to server C. If servers A and B finish their tasks and are now handling 1 connection each, the next request will go to either A or B.

3. **IP Hash**: This method uses the client's IP address to determine which server to forward the request to. The load balancer applies a hash function to the client's IP address and uses the result to map the request to one of the servers. This method ensures that a particular client (IP address) always reaches the same server, as long as no servers are added or removed. This can be useful for maintaining client-specific data like sessions or caches on the server. For example, if client with IP 192.168.1.1 results in hash value 2 and you have 3 servers, the request will be forwarded to server 2. If the same client sends another request, it will again be forwarded to server 2.
---
**what happens if a new server is added and this scenario is no longer valid "as long as no servers are added or removed"?**

When a new server is added or removed in a load balancing scenario using the IP Hash method, the distribution of requests can change significantly. This is because the hash function will produce a different result when the number of servers changes.

For example, let's say you have 3 servers and a client with IP address 192.168.1.1. The hash function might map this IP address to server 2. Now, if a new server is added, making it 4 servers in total, the hash function might map the same IP address to a different server, say server 3.

This can disrupt session persistence for some clients, as they might get directed to a different server where their session data doesn't exist. This is one of the drawbacks of the IP Hash method. If session persistence is critical for your application, you might need to consider other load balancing methods or use a shared session store that all servers can access.

----

**Consistent hashing**
Consistent hashing is a special kind of hashing technique that is primarily used in distributed systems to achieve better load distribution among multiple nodes (like servers). It minimizes the reorganization of keys when nodes are added or removed, thus reducing the need for data movement and providing better performance and scalability.

In traditional hashing, when the hash table is resized (i.e., when nodes are added or removed), most keys will hash to a new location, leading to a potential massive relocation of data. In contrast, consistent hashing ensures that when a node is added or removed, only a minimal number of keys are remapped to different nodes.

Here's how it works:

1. Imagine a circle (often called a "ring") where each point on the circle corresponds to a hash value. The range of hash values is the same as the output range of the hash function used.

2. Each node (server) in the system is assigned a hash value by hashing its identifier. This determines its position on the edge of the circle.

3. To find where a given key should be stored, you hash the key, which gives you a position on the edge of the circle. You then move around the circle until you find a node. The key is stored on that node.

4. When a node is added, it takes over some of the keys from its neighbors. When a node is removed, its keys are taken over by its neighbors. In both cases, all other nodes are unaffected.

Consistent hashing is used in many distributed systems, including distributed caches, distributed file systems, and more. It's also used in some load balancing schemes.

However, in the context of the load balancing methods we discussed earlier (Round Robin, Least Connections, IP Hash), consistent hashing is not directly used. These methods have their own ways of distributing load, and they don't involve a hash ring or keys being assigned to nodes.

That said, there are load balancing schemes that do use consistent hashing. For example, some distributed caches use consistent hashing to distribute keys among cache nodes. And some load balancers use a variant of consistent hashing for "sticky sessions", where requests from the same client are always routed to the same server. But these are more advanced topics that go beyond the basic load balancing methods we discussed earlier.


[What is CONSISTENT HASHING and Where is it used? - YouTube](https://www.youtube.com/watch?v=zaRkONvyGr8&ab_channel=GauravSen)
K hash functions for rendering virtual servers.
 
----
Load balancers can be implemented in several ways, including through smart clients, hardware load balancers, and software load balancers. Here's a brief overview of each:

1. **Smart Clients**: In this approach, the client itself is responsible for choosing which server to send requests to. The client has a list of available servers and uses some algorithm to choose one for each request. This could be as simple as round-robin selection, or it could involve more complex logic like taking into account the current load on each server. This approach requires no special hardware or software on the server side, but it does require more logic in the client.

2. **Hardware Load Balancers**: These are physical devices that sit between the client and the servers. They receive incoming network traffic and distribute it to a server based on a configured algorithm. Hardware load balancers are typically used in high-traffic environments because they can handle a large amount of network traffic and offer high performance and reliability. However, they can be expensive and may require specialized knowledge to configure and maintain.

3. **Software Load Balancers**: These are programs that run on a server and distribute incoming network traffic to other servers. Software load balancers can be more flexible and easier to configure than hardware load balancers. They can also be less expensive, especially if you use open-source software. However, they may not be able to handle as much network traffic as a hardware load balancer, and they can consume resources on the server where they're running.

---
Types of LB:

- Least Connection: This algorithm directs traffic to the server with the fewest active connections. It's useful in situations where sessions are long and vary in the processing time required.  
- Least Response Time: This algorithm directs traffic to the server with the fewest active connections and the lowest average response time. It's useful when there are a significant number of persistent connections in the traffic managed by the load balancer.  
- Least Bandwidth: This algorithm directs traffic to the server that is currently serving the least amount of traffic measured in megabits per second (Mbps).  
- Round Robin: This algorithm cycles through a list of servers and sends each new request to the next server. When it reaches the end of the list, it starts over at the beginning. It's simple and works well when the servers are of equal specification and there are not many persistent connections.  
- Weighted Round Robin: This is an extension of the round-robin algorithm. In this case, each server is assigned a weight based on its processing capacity. Servers with higher weights receive new connections first and get more connections than servers with lower weights. Servers with equal weights get an equal distribution of new connections.  
- IP Hash: This algorithm uses the client's IP address to determine which server receives the request. The client's IP address is hashed to a server. All of a client's requests are sent to the same server. This method ensures that a client will always connect to the same server as long as no servers are added or removed. 
---
