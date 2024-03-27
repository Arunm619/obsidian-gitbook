
[CS75 (Summer 2012) Lecture 9 Scalability Harvard Web Development David Malan - YouTube](https://youtu.be/-W9F__D3oY4?t=388)

#### Web hosting Services & Virtual Private Services

**Problem:**
Web hosting is a service that allows organizations and individuals to post a website or web page onto the Internet. A web host, or web hosting service provider, is a business that provides the technologies and services needed for the website or webpage to be viewed on the Internet. Websites are hosted, or stored, on special computers called servers.

**Solution:**
Web hosting solutions provide the server space and technology needed for your website to be accessed over the Internet. They store your website files and deliver them to the browsers of your users. There are different types of web hosting solutions available, such as shared hosting, dedicated hosting, VPS hosting, and cloud hosting.

**Advantages:**
- **Ease of Use:** Most web hosting solutions provide easy-to-use interfaces or control panels. You can upload your website, install CMS platforms, set up email accounts, and more.
- **Technical Maintenance:** The web hosting provider takes care of server maintenance. This includes everything from hardware replacement to software updates.
- **Scalability:** As your website grows, you can upgrade your hosting plan to accommodate more traffic and complexity.
- **Support:** Most web hosting providers offer 24/7 technical support to help you with any issues you encounter.

**Disadvantages:**
- **Cost:** While some hosting plans are quite affordable, others, especially dedicated and managed hosting, can be quite expensive.
- **Limited Resources:** On shared hosting plans, resources such as memory, CPU time, and disk space are shared among all the websites on the server. This can lead to slower website performance, especially if one of the websites uses a lot of resources.
- **Security Risks:** Sharing server space with other websites can pose a security risk if one of the other websites is compromised.

**Providers in the Market:**
- **Bluehost:** Known for their excellent customer service and great uptime.
- **HostGator:** Offers a range of plans, including shared hosting, VPS hosting, and dedicated servers.
- **SiteGround:** Known for their excellent uptime and strong security features.
- **GoDaddy:** Offers a wide range of products, including domain registration, shared hosting, and dedicated servers.
- **Amazon Web Services (AWS):** Offers a broad set of global compute, storage, database, analytics, application, and deployment services.


----
#### Vertical Scaling (scaling up)

**Vertical Scaling**, also known as "scaling up", is a method of increasing the capacity of a server or a database by adding resources to it. These resources can be in the form of CPU, RAM, or disk storage. The main idea behind vertical scaling is to increase the power of a single server to handle more load.

1. **Hardware Upgrade:** Vertical scaling often involves adding more powerful hardware to an existing server. This could mean upgrading the server's CPU, adding more RAM, or increasing the server's storage capacity.

2. **Software Optimization:** Vertical scaling can also involve optimizing the software running on the server to make better use of the server's resources. This could involve tuning the server's operating system, optimizing the server's database configuration, or tweaking the server's network settings.

3. **Single Point of Failure:** One of the main drawbacks of vertical scaling is that it can create a single point of failure. If the server goes down, all services running on that server will be unavailable until the server is back online.

4. **Limited by Hardware:** Vertical scaling is ultimately limited by the maximum capacity of the server's hardware. Once the server's hardware is fully utilized, the only option is to add more servers (horizontal scaling).

5. **Downtime:** Vertical scaling often requires downtime while the server's hardware is upgraded or the server's software is optimized.

6. **Cost:** Upgrading a server's hardware can be expensive, especially if high-end components are required. Additionally, the cost of maintaining a single, powerful server can be higher than maintaining multiple, less powerful servers.

7. **Performance Improvement:** Despite its drawbacks, vertical scaling can significantly improve the performance of a server or a database. By adding more resources to a server, it can handle more simultaneous requests, process data faster, and store more data.

In the context of web hosting, vertical scaling would involve upgrading the server that hosts the website to handle more traffic or store more data. This could involve upgrading the server's CPU, adding more RAM, or increasing the server's storage capacity.


----
#### Horizontal scaling (Scaling out)

**Horizontal Scaling**, also known as "scaling out", is a method of increasing the capacity of a system by adding more servers or nodes to the system. Unlike vertical scaling, which focuses on increasing the capacity of a single server, horizontal scaling involves adding more servers to distribute the load.

**Details of Horizontal Scaling:**

1. **Adding More Servers:** Horizontal scaling involves adding more servers to a system. These servers work together to serve the application, distributing the load among them. This can be done by adding more physical servers, or by adding more virtual servers in a cloud environment.

2. **Load Balancing:** In a horizontally scaled system, a load balancer is often used to distribute the incoming requests to the servers. The load balancer ensures that no single server becomes a bottleneck, improving the overall performance and reliability of the system.

3. **Data Distribution:** In a horizontally scaled system, data is often distributed across the servers. This can be done using techniques like sharding, where each server holds a portion of the total data.

4. **Fault Tolerance:** One of the main advantages of horizontal scaling is increased fault tolerance. If one server fails, the system can continue to operate using the remaining servers. This is in contrast to vertical scaling, where the failure of a single server can bring down the entire system.

5. **Scalability:** Horizontal scaling allows a system to handle more traffic by simply adding more servers. This makes it a good choice for systems that need to handle large amounts of traffic or data.

6. **Cost:** While adding more servers can be expensive, it can also be more cost-effective than vertical scaling in the long run. This is because the cost of servers can decrease over time, and it's often cheaper to add more lower-cost servers than to upgrade a single server to a more powerful (and expensive) model.

7. **Complexity:** One of the main challenges of horizontal scaling is the increased complexity. Managing multiple servers, distributing data, and balancing load can all add complexity to a system.

In the context of web hosting, horizontal scaling would involve adding more servers to host the website. This could involve adding more physical servers, or adding more virtual servers in a cloud environment. The load balancer would distribute the incoming traffic to the servers, ensuring that no single server becomes a bottleneck.


----

#### nslookup 

`nslookup` is a network administration command-line tool available for many computer operating systems. It is used for querying the Domain Name System (DNS) to obtain domain name or IP address mapping, or other DNS records. 

The name "nslookup" means "name server lookup". This tool is commonly used for troubleshooting DNS servers, checking DNS records, and finding IP addresses of specific web servers or other domain names. 

Here's a basic usage example:

```bash
nslookup www.example.com
```

This command will return the IP address associated with the domain `www.example.com`

Please note that `nslookup` is gradually being deprecated and replaced by other tools such as `dig` in many systems, but it's still widely used and available on many systems.

```english
❯ nslookup images.meesho.com
Server:		192.168.1.1
Address:	192.168.1.1#53

Non-authoritative answer:
Name:	images.meesho.com
Address: 34.111.251.190

~ ─────────────────────────────────────────────────────────────────
❯ nslookup 34.111.251.190
Server:		192.168.1.1
Address:	192.168.1.1#53

Non-authoritative answer:
190.251.111.34.in-addr.arpa	name = 190.251.111.34.bc.googleusercontent.com.

Authoritative answers can be found from:
111.34.in-addr.arpa	nameserver = ns-gce-public2.googledomains.com.
111.34.in-addr.arpa	nameserver = ns-gce-public4.googledomains.com.
111.34.in-addr.arpa	nameserver = ns-gce-public1.googledomains.com.
111.34.in-addr.arpa	nameserver = ns-gce-public3.googledomains.com.
ns-gce-public1.googledomains.com	internet address = 216.239.32.102
ns-gce-public2.googledomains.com	internet address = 216.239.34.102
ns-gce-public3.googledomains.com	internet address = 216.239.36.102
ns-gce-public4.googledomains.com	internet address = 216.239.38.102
ns-gce-public1.googledomains.com	has AAAA address 2001:4860:4802:32::66
ns-gce-public2.googledomains.com	has AAAA address 2001:4860:4802:34::66
ns-gce-public3.googledomains.com	has AAAA address 2001:4860:4802:36::66
ns-gce-public4.googledomains.com	has AAAA address 2001:4860:4802:38::66
```

---

#### RAID 

RAID stands for Redundant Array of Independent Disks. It's a method of storing the same data in different places on multiple hard disks or solid-state drives to protect data in the case of a drive failure. 

There are several different RAID levels, each with different advantages and trade-offs in terms of data redundancy, performance, and capacity:

1. **RAID 0** – Striped Disk Array without Fault Tolerance: 
   - Advantages: Provides improved performance due to data striping, where blocks of each file are spread out across multiple disk drives. This allows for faster data reading and writing.
   - Trade-offs: There's no redundancy in RAID 0, so if one drive fails, all data is lost. It's not recommended for critical data storage.

2. **RAID 1** – Mirroring and Duplexing: 
   - Advantages: Provides disk mirroring, which means all data is written identically on two drives. This offers high data protection and can double the read speed.
   - Trade-offs: The write speed is the same as for single disks, and it requires twice the storage capacity to store all data.

3. **RAID 5** – Block Interleaved Distributed Parity: 
   - Advantages: Provides a good balance of performance, storage capacity, and data integrity. Data and parity (error checking) information are striped across three or more drives. If a single drive fails, the data can be rebuilt from the parity information.
   - Trade-offs: Write operations are slower due to the need to write parity information. Also, if two drives fail simultaneously, all data is lost.

4. **RAID 6** – Independent Data Disks with Double Parity: 
   - Advantages: Similar to RAID 5, but includes a second parity block distributed across drives, offering extra fault tolerance. It can withstand the loss of two drives.
   - Trade-offs: Write operations can be slower due to the extra parity data. It requires a minimum of four drives, so initial costs are higher.

5. **RAID 10** – A Stripe of Mirrors: 
   - Advantages: Combines the advantages of RAID 0 (striping) and RAID 1 (mirroring). It provides high data protection and improved performance, and can withstand multiple drive failures.
   - Trade-offs: Requires at least four drives and offers only 50% storage efficiency, as all data is duplicated.

6. **RAID 50** – Combines the straight block-level striping of RAID 0 with the distributed parity of RAID 5.
   - Advantages: It provides a good balance of performance, storage capacity, and data integrity. It can withstand a single drive failure within each RAID 5 array.
   - Trade-offs: It requires a minimum of six drives and the loss of two drives in the same RAID 5 array will result in data loss.

7. **RAID 60** – Combines the straight block-level striping of RAID 0 with the distributed double parity of RAID 6.
   - Advantages: It provides very high data fault tolerance and can withstand multiple drive failures.
   - Trade-offs: It requires a minimum of eight drives and has high parity overhead, which can slow down write operations.

The choice of RAID level depends on the specific needs and constraints of the system, including the criticality of the data, budget, performance requirements, and storage capacity.

----

#### Is RAID still valid in SSD era?
Yes, the concept of RAID (Redundant Array of Independent Disks) is still applicable in the era of Solid State Drives (SSDs). RAID is a method of storing the same data in different places on multiple hard disks or SSDs to protect data in the case of a drive failure. 

While SSDs are generally more reliable and faster than traditional hard drives, they can still fail for a variety of reasons such as wear and tear, power surges, or manufacturer defects. Therefore, using RAID with SSDs can provide the same benefits as with hard drives, including data redundancy, improved performance, and increased storage capacity.

However, there are some considerations when using RAID with SSDs:

1. **Wear Leveling**: SSDs have a finite number of write cycles. In a RAID setup, especially in RAID levels that involve a lot of writing like RAID 5 and 6, this could potentially lead to faster wear of the SSDs.

2. **TRIM Support**: TRIM is a command that allows an operating system to inform an SSD which blocks of data are no longer considered in use and can be wiped. This is important for maintaining the performance of an SSD. However, not all RAID controllers support the TRIM command.

3. **Cost**: SSDs are more expensive than hard drives in terms of cost per gigabyte. Therefore, setting up a RAID array with SSDs can be more costly.

In conclusion, while the concept of RAID is still valid for SSDs, the implementation might require additional considerations compared to traditional hard drives.


----
#### How to implement LB

There are several pre-existing solutions for implementing load balancers. Here are a few popular ones:

1. **NGINX**: NGINX is a popular open-source software that can be used as a load balancer, as well as a reverse proxy server, and an HTTP cache. It supports various load balancing algorithms, SSL termination, health checks, and more.

2. **HAProxy**: HAProxy is another open-source software that provides high availability, load balancing, and proxy for TCP and HTTP-based applications. It is well-known for its high performance and stability.

3. **Amazon Elastic Load Balancing (ELB)**: If you're hosting your application on AWS, you can use ELB to automatically distribute incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, and IP addresses.

4. **Google Cloud Load Balancing**: For applications hosted on Google Cloud, you can use their load balancing service to distribute traffic in single or multiple regions, close to the user, to meet your high availability requirements.

5. **Azure Load Balancer**: For applications on Microsoft Azure, you can use Azure Load Balancer to scale your applications and create high availability for your services.

6. **Kubernetes Services**: If you're using Kubernetes, it has a built-in service abstraction that can automatically distribute network traffic to pods based on IP and the port on which they expose their app.

Each of these solutions has its own setup and configuration process, and the best one for you depends on your specific needs and the environment in which your application is running.


-----
#### How does a system store the user session data in a distributed server architecture?


In a distributed server architecture, user session data can be stored using several methods. Here are a few common ones:

1. **In-Memory Data Stores (like Redis or Memcached)**: These are high-performance, distributed memory object caching systems that store data in memory, reducing the need to access data from disk. They are often used to store session data in a distributed environment. However, data stored in memory can be lost if the server crashes or restarts.

2. **Database**: Session data can be stored in a centralized database that all servers in the distributed system can access. This can be a SQL or NoSQL database depending on the application's requirements. The downside is that database operations can be slower than in-memory operations, and it can become a bottleneck if not properly managed.

3. **Sticky Sessions**: With sticky sessions, once a client starts a session with a specific server, all subsequent requests from that client during the session are sent to the same server. This allows the server to store session data in its local memory. However, this approach can lead to uneven load distribution and doesn't provide a good solution if the server crashes or needs to be taken down for maintenance.

4. **Distributed Cache**: Distributed caches like Hazelcast or Apache Ignite can store session data across a cluster of servers. They automatically partition the data and provide redundancy, so if one server fails, the session data is not lost.

5. **JWT (JSON Web Tokens)**: Instead of storing session data on the server, it can be stored on the client side in a JWT. The JWT is signed by the server, so the client can't tamper with it. When the client makes a request, it includes the JWT, and the server can verify it and extract the session data. This stateless approach scales well, but it's not suitable for all applications, especially if the session data is large.

---
#### JWT 

JSON Web Tokens (JWT) are an open, industry standard (RFC 7519) method for representing claims securely between two parties. JWTs are commonly used for authorization. Once a user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token.

A JWT is composed of three parts: a header, a payload, and a signature.

1. **Header**: The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.

2. **Payload**: The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data.

3. **Signature**: To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

Here's an example of how you might generate and verify JWTs in Kotlin using the `jose4j` library:

```kotlin
import org.jose4j.jws.AlgorithmIdentifiers
import org.jose4j.jws.JsonWebSignature
import org.jose4j.jwt.JwtClaims
import org.jose4j.jwt.consumer.JwtConsumer
import org.jose4j.jwt.consumer.JwtConsumerBuilder
import org.jose4j.keys.HmacKey

fun generateJWT(secret: String, claim: String): String {
    val claims = JwtClaims()
    claims.setClaim("customClaim", claim)

    val jws = JsonWebSignature()
    jws.payload = claims.toJson()
    jws.key = HmacKey(secret.toByteArray())
    jws.algorithmHeaderValue = AlgorithmIdentifiers.HMAC_SHA256

    return jws.compactSerialization
}

fun verifyJWT(jwt: String, secret: String): Boolean {
    val jwtConsumer = JwtConsumerBuilder()
        .setRequireExpirationTime()
        .setAllowedClockSkewInSeconds(30)
        .setRequireSubject()
        .setExpectedIssuer("Issuer")
        .setExpectedAudience("Audience")
        .setVerificationKey(HmacKey(secret.toByteArray()))
        .build()

    return try {
        val claims = jwtConsumer.processToClaims(jwt)
        claims.getClaimValue("customClaim") != null
    } catch (e: Exception) {
        false
    }
}
```

In this example, `generateJWT` creates a JWT with a custom claim and `verifyJWT` verifies the JWT and checks if the custom claim exists. The secret used to sign the JWT should be the same for both generating and verifying the JWT.


----

#### Data replication 

Data replication is a method of copying data from one location to another to ensure consistency between redundant resources, such as software or hardware, to improve reliability, fault-tolerance, or accessibility. There are two main types of data replication: active-passive and active-active.  

- Active-Passive Replication: In this model, one server (the active server) handles all the requests while the other server (the passive server) is on standby. The active server continuously updates the passive server with data changes. If the active server fails, the passive server takes over. This model ensures high availability but doesn't distribute the load.  

- Active-Active Replication: In this model, all servers are active and can handle requests. Data changes on any server are propagated to all other servers. This model provides both high availability and load distribution, but it's more complex because it requires conflict resolution if the same data is changed on multiple servers at the same time.


---

#### Data center redundancy

 Data center redundancy is a strategy used in data centers to ensure that a backup or failover system is in place in case the primary systems fail. This is crucial for maintaining data availability and minimizing downtime. There are several levels of redundancy, commonly referred to as N, N+1, 2N, and 2N+1.

1. **N**: This is the minimum capacity required to run your data center. There is no redundancy in this model.

2. **N+1**: This model has one additional component as a backup for each component in your data center. If a component fails, the backup component takes over.

3. **2N**: This model has a full set of backup components for your entire data center. If any component or even the entire data center fails, the backup can take over.

4. **2N+1**: This model is similar to 2N but has an extra component for each component in your data center. This provides even more reliability.

In terms of data center design, redundancy can be applied to various components such as power supplies, cooling systems, network links, storage systems, and servers. The level of redundancy you choose depends on the criticality of the applications running in your data center and your budget.

For example, in a software application, redundancy can be achieved by using multiple servers in an active-active or active-passive configuration, as discussed in the previous conversation. In an active-active configuration, all servers are active and can handle requests. In an active-passive configuration, one server handles all the requests while the other server is on standby.


---

#### Security

Security in a distributed system is a critical aspect that ensures the integrity, confidentiality, and availability of data and services. Here are some key concepts related to security in distributed systems:

1. **Authentication**: This is the process of verifying the identity of a user, device, or system. It often involves the use of usernames and passwords, tokens, or certificates.

2. **Authorization**: Once a user, device, or system is authenticated, they must be authorized. This is the process of giving the authenticated entity permission to access certain data or services.

3. **Data Integrity**: This ensures that the data is real, accurate, and safeguarded from unauthorized user modifications.

4. **Confidentiality**: This ensures that the data or service is accessible only to authorized users and systems.

5. **Availability**: This ensures that the data or services are always available to the users when needed.

In the context of your project, you can implement these security measures in various ways.

For instance, you can use **JWT (JSON Web Tokens)** for authentication and authorization. JWTs are secure because they are digitally signed, and they can carry all the necessary data to authenticate and authorize a user.

For data integrity and confidentiality, you can use **encryption techniques** to encrypt the data before storing or transmitting it. This ensures that even if an unauthorized user gains access to the data, they cannot understand it without the decryption key.

For availability, you can use techniques like **data replication and redundancy**. For example, you can have multiple instances of your services running in different locations. If one instance fails, the others can continue to provide the service.

----
#### IP address and Port

An IP address (Internet Protocol address) is a unique identifier for a device on a network. It's used to locate and identify the device among billions of devices connected to the Internet. There are two types of IP addresses: IPv4 and IPv6. 

- IPv4 addresses are most commonly used and are written as four sets of numbers, each ranging from 0 to 255, separated by periods (e.g., 192.168.1.1).
- IPv6 addresses were introduced to deal with the long-anticipated problem of IPv4 address exhaustion and are written as eight groups of four hexadecimal digits, separated by colons.


A Port is a communication endpoint in the context of networking. When a service listens for incoming connections from the network, it is said to **bind** to a port. 

- Each port is associated with a specific process or service and is identified by a port number, a 16-bit integer, which means they can range from 0 to 65535.
- However, ports 0 to 1023 are known as well-known ports and are reserved for privileged services and designated as well-known by the Internet Assigned Numbers Authority (IANA).

In the context of a client-server model, an IP address helps the client find the server on the network, and the port number helps the client find the specific service on the server it wants to communicate with. 
For example, web servers typically listen on port 80 for HTTP and port 443 for HTTPS.

| Service | Port | Description |
|---------|------|-------------|
| HTTP | 80 | Default port for web servers that use HTTP |
| HTTPS | 443 | Default port for web servers that use HTTPS |
| FTP | 20, 21 | Ports used for File Transfer Protocol. Port 20 is used for data transfer, and port 21 is used for control |
| SSH | 22 | Used for Secure Shell, a protocol used for secure remote login and other secure network services over an insecure network |
| Telnet | 23 | Used for Telnet, a protocol used for interactive communication with another host using the TELNET protocol |
| SMTP | 25 | Used for Simple Mail Transfer Protocol, a protocol for sending email messages between servers |
| DNS | 53 | Used for Domain Name System services |
| DHCP | 67, 68 | Used for Dynamic Host Configuration Protocol. Port 67 is used by the DHCP server, and port 68 is used by the DHCP client |
| POP3 | 110 | Used for Post Office Protocol, used by email clients to retrieve mail from a server |
| IMAP | 143 | Used for Internet Message Access Protocol, used by email clients to retrieve mail from a server |
| LDAP | 389 | Used for Lightweight Directory Access Protocol, used for accessing and maintaining distributed directory information services over an Internet Protocol (IP) network |
| MySQL | 3306 | Used for MySQL database service |
| PostgreSQL | 5432 | Used for PostgreSQL database service |
| MongoDB | 27017 | Used for MongoDB, a NoSQL database |

----

#### Firewalls

A firewall is a network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. It establishes a barrier between a trusted internal network and untrusted external network, such as the Internet.

Firewalls can be hardware, software, or both. They are used to prevent unauthorized access to or from a private network. Firewalls can be configured to block data from certain locations or applications while allowing relevant and necessary data through.

Firewalls are a crucial component of comprehensive security frameworks and are often the first line of defense in network security. They can protect against various security threats like malicious software, hackers, and viruses.

Configuring a firewall to allow specific network traffic depends on the type of firewall you are using. However, the general process involves defining rules that specify which type of traffic is allowed. Here's a general step-by-step process:

1. Identify the type of traffic you want to allow. This could be based on the IP address, port number, or protocol (TCP, UDP, etc.).

2. Access your firewall's configuration settings. This process will vary depending on whether you're using a software or hardware firewall, and the specific product you're using.

3. Look for a section where you can define rules or policies. This is often called something like "Inbound Rules", "Access Rules", or "Policies".

4. Create a new rule. Specify the details of the traffic you want to allow. This will typically involve entering the IP address, port number, and protocol.

5. Save the rule and apply the changes. Your firewall should now allow the specified network traffic.

For example, if you're using a Unix-like operating system, you might use the `iptables` command to configure the firewall. Here's an example command that allows incoming traffic on port 80 (commonly used for HTTP):

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

In this command:

- `-A INPUT` adds a rule to the INPUT chain (for incoming traffic).
- `-p tcp` specifies the protocol (TCP).
- `--dport 80` specifies the destination port (port 80).
- `-j ACCEPT` specifies the target of the rule (ACCEPT the packet).

Please replace the port number and protocol as per your requirements. Also, remember that these changes are not persistent across reboots. To make them persistent, you would need to save these rules to a file and restore them when the system boots.

Remember, modifying firewall rules can have significant security implications. Always ensure you understand the changes you're making and consider their potential impact on your network's security.


To ensure that only port 3306 is open from your server to a database server, you can use firewall rules. The specific commands depend on the operating system and the firewall software you're using. 

For example, if you're using a Unix-like operating system with `iptables`, you can use the following commands:

```bash
# First, block all outgoing connections:
iptables -P OUTPUT DROP

# Then, allow outgoing connections on port 3306:
iptables -A OUTPUT -p tcp --dport 3306 -j ACCEPT

# Finally, save the changes:
service iptables save
```

This will block all outgoing connections except those going to port 3306. 

Please replace `iptables` with the appropriate command for your firewall software if you're not using `iptables`. Also, you might need to run these commands with `sudo` or as root, depending on your system's configuration.

Remember to replace the port number with the one you want to allow if it's not 3306. Also, this is a very restrictive setup – it blocks all outgoing connections except for the specified port. Depending on your server's role, this might not be what you want. 

Please note that managing firewall rules can have significant effects on your system and can cause network-related features to stop working if not done correctly. Always double-check the rules and consider all the implications before applying them.

---

