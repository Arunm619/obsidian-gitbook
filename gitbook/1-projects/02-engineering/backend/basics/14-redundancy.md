
- Redundancy: **duplication of critical data or services** with the intention of increased reliability of the system.
- Server failover
	  - Remove single points of failure and provide backups (e.g. server failover).
- Shared-nothing architecture
	  - Each node can operate independently of one another.
	  - No central service managing state or orchestrating activities.
	  - New servers can be added without special conditions or knowledge.
	  - No single point of failure.

---


In a distributed system, redundancy, server failover, and shared-nothing architecture are crucial concepts that ensure the system's reliability, availability, and scalability. 

1. **Redundancy**: This involves duplicating critical components or data across multiple systems. If one system fails, the redundant system can take over, ensuring that the service remains available. In a distributed system, redundancy can be achieved at various levels, such as data redundancy (replicating databases), service redundancy (running multiple instances of a service), and hardware redundancy (having backup servers).

2. **Server Failover**: This is a process where a secondary system becomes active when the primary system fails, ensuring the continuity of the service. In a distributed system, server failover can be automated using health checks and load balancers. Health checks monitor the status of the servers, and if a server fails, the load balancer redirects the traffic to the backup server.

3. **Shared-Nothing Architecture**: In this architecture, each node in the system operates independently of the others. There's no central service managing state or orchestrating activities. This architecture is highly scalable because new servers can be added without special conditions or knowledge. It also eliminates single points of failure because even if one node fails, the others can continue to operate.

Here's a simple example of how you might implement these concepts in a distributed system using Kotlin and Ktor, a Kotlin framework for building asynchronous servers and clients:

```kotlin
import io.ktor.application.*
import io.ktor.response.*
import io.ktor.routing.*
import io.ktor.server.engine.*
import io.ktor.server.netty.*

fun main() {
    // Start two instances of the server for redundancy
    startServer(port = 8080)
    startServer(port = 8081)
}

fun startServer(port: Int) {
    embeddedServer(Netty, port = port) {
        routing {
            get("/") {
                call.respondText("Hello, World!")
            }
        }
    }.start(wait = false)
}
```

In this example, we're starting two instances of a simple Ktor server on different ports. This provides redundancy - if one server goes down, the other can continue to handle requests. It also demonstrates a shared-nothing architecture, as each server instance operates independently of the others.

For server failover, you would typically use a load balancer (not shown in this example). The load balancer would monitor the health of the servers and distribute incoming requests between them. If one server fails, the load balancer would stop sending requests to it and redirect all traffic to the remaining server.
