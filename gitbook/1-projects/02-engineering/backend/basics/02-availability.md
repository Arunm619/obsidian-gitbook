
-  Availability is the time a system remains operational to perform its required function in a specific period.
- Measured by the percentage of time that a system remains operational under normal conditions.
- A reliable system is available.
- An available system is not necessarily reliable.
  - A system with a security hole is available when there is no security attack.

This statement highlights an important distinction between availability and reliability in systems, particularly in the context of security.

1. **Availability vs. Reliability**:
    
    - **Availability** refers to the accessibility and usability of a system or service. It means that the system is operational and can be used when needed.
    - **Reliability**, on the other hand, refers to the consistency and dependability of a system. A reliable system consistently performs its intended functions correctly without failure over a specified period.
2. **Security Hole and Availability**:
    
    - A system with a security hole can still be available if it is accessible and operational. In other words, users can still access the system despite the presence of vulnerabilities.
    - The existence of a security hole does not necessarily mean that the system will be unavailable. It may continue to function and be accessible to users.
3. **Security Attack and Reliability**:
    
    - However, the presence of a security hole compromises the reliability of the system. It introduces a risk of security attacks, such as unauthorized access, data breaches, or service interruptions.
    - A successful security attack can disrupt the system's normal operations, leading to downtime or loss of data, thereby affecting its reliability.



----

Availability in the context of software systems refers to the system being accessible and operational when users need it. It's a measure of the time a system is up and running, often expressed as a percentage of the total time. For instance, a system with 99.999% availability is said to have "five nines" of availability, meaning it's down for no more than about 5 minutes per year.

High availability is a key goal in the design of software systems, especially those that are mission-critical or serve a large number of users. Achieving high availability involves several strategies:

1. **Redundancy**: This involves having multiple instances of the same component (such as servers or databases), so that if one fails, others can take over. This can be within the same data center or spread across multiple geographical locations.

2. **Load Balancing**: This is a technique used to distribute workloads across multiple computing resources, such as servers or hard drives. This not only helps in achieving redundancy but also helps in optimizing resource use, maximizing throughput, and minimizing response time.

3. **Failover**: This is the process of switching to a redundant or standby system in the event of a failure. The goal is to enable the system to continue operation even after a failure.

4. **Monitoring and Health Checks**: Regular checks are performed to ensure that all components of the system are functioning correctly. If a problem is detected, it can be addressed immediately, before it leads to downtime.

5. **Maintenance and Updates**: Regular maintenance and updates are crucial to ensure the system remains available. This includes patching software vulnerabilities, updating system components, and performing routine checks and optimizations.

In the context of a backend system written in Kotlin or Java, you might use frameworks and libraries that support these strategies. For instance, Spring Boot, a popular framework for building Java applications, provides features for building highly available, fault-tolerant systems.

Here's a simple example of a Spring Boot application with a health check endpoint:

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

    @Bean
    public HealthIndicator myHealthIndicator() {
        return () -> Health.up().withDetail("Everything", "is ok").build();
    }
}
```

In this example, Spring Boot Actuator is used to expose a health check endpoint (`/actuator/health`). This endpoint can be used by monitoring tools to check the health of the application. If the application becomes unhealthy, it can be restarted or replaced to maintain availability.



---

the concept of "nines" in availability is a way to express the uptime of a system as a percentage. The more nines, the higher the availability and the less downtime a system has over a given period. Here's a table that breaks down what each level of "nines" means in terms of downtime over a year:

| Nines | Availability | Downtime per Year |
|-------|--------------|-------------------|
| One Nine | 90% | More than 36 days |
| Two Nines | 99% | Less than 4 days |
| Three Nines | 99.9% | Less than 9 hours |
| Four Nines | 99.99% | Less than 1 hour |
| Five Nines | 99.999% | Less than 5 minutes |
| Six Nines | 99.9999% | Less than 31 seconds |

As you can see, each additional nine significantly reduces the amount of acceptable downtime. Achieving high levels of availability (like five or six nines) requires careful planning, robust system architecture, and often comes with increased cost.


----

#### How to measure availability

Measuring availability is a single percentage metric. It is the total elapsed time minus the total downtime divided by the total elapsed time:

**availability percentage = (total elapsed time – downtime) / total elapsed time**

For example, if an online retail site is down for three hours in a day due to traffic overload, its availability score is 87.5%. The standard may be closer to 99.5% for large international retailers, giving the online retailer much to improve.


---
