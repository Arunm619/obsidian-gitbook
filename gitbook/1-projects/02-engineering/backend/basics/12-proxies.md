
- A proxy server is an intermediary piece of hardware / software sitting between client and backend server.
    - Filter requests
    - Log requests
    - Transform requests (encryption, compression, etc)
    - [Cache](https://github.com/Jeevan-kumar-Raj/Grokking-System-Design/blob/master/basics/caching.md)
    - Batch requests
        - Collapsed forwarding: enable multiple client requests for the same URI to be processed as one request to the backend server
        - Collapse requests for data that is spatially close together in the storage to minimize the reads

---

Forward proxy Vs Reverse Proxy 

Forward proxy - VPN in mobile phones , masking client 
Reverse Proxy - Load balancer that masks the web/app servers.

---

A proxy server in system design is a server that acts as an intermediary for requests from clients seeking resources from other servers. It provides a layer of security, functionality, and privacy depending on the use case.

There are several types of proxy servers:

1. **Forward Proxy**: This is the most common type of proxy server and is often simply referred to as a "proxy". It sits between the client and the internet, with the client requests going out to the internet via the proxy server.

2. **Reverse Proxy**: This type of proxy server sits in front of web servers and forwards client (e.g. web browser) requests to those web servers. Reverse proxies are useful for load balancing, web acceleration, and security.

3. **Open Proxy**: An open proxy is a type of forward proxy that is openly available to any internet user. Most often, these are used to serve as a web cache or to anonymize web browsing.

4. **Data Center Proxy**: These are the proxies that are not affiliated with an Internet Service Provider (ISP) but a third-party provider. They are reliable, fast, and come from a reliable source.

5. **Residential Proxy**: These are IP addresses provided by an ISP and are assigned to homeowners. They are legitimate IP addresses and are less likely to be blocked by websites.

**Advantages of using a proxy server:**

1. **Control internet usage of employees and children**: This is especially applicable in corporate and educational settings. Network administrators can restrict access to certain websites or types of content.

2. **Bandwidth savings and improved speeds**: Proxy servers can cache (save a copy of the website locally) popular websites, so when you ask for www.google.com, the proxy server will check to see if it has the most recent copy of the site, and then send you the saved copy.

3. **Privacy benefits**: Individuals and organizations alike use proxy servers to browse the internet more privately. Some proxy servers will change the IP address and other identifying information the web request contains.

4. **Security**: Proxy servers provide security benefits on top of privacy benefits. You can configure your proxy server to encrypt your web requests to keep prying eyes from reading your transactions.

Disadvantages of using a proxy server:

1. **Performance can be affected**: Proxy servers can also make your Internet access slower, depending on the amount of traffic they are handling at any given time.

2. **Security risks**: While proxy servers can provide more layers of security, they can also be a security risk. If you're using a proxy server that isn't secure, your information may not be protected.

3. **Cost**: While there are some free proxy servers available, many of the services available do cost money. This cost can be recurring monthly or yearly and adds up over time.

4. **Complexity**: Setting up a proxy server can be quite complex and might require specialized knowledge.


---
#### What are some common use cases for reverse proxy servers?

Reverse proxy servers are commonly used in system design for several purposes:

1. **Load Balancing**: A reverse proxy server can distribute client requests across multiple servers. This helps to balance the load on the servers, preventing any one server from becoming a bottleneck, and thus improving performance and reliability.

2. **SSL Termination**: Handling SSL encryption and decryption (converting the encrypted data coming from the internet into a format that your back-end systems can understand) can be a computationally expensive process. A reverse proxy server can be used to handle this process, freeing up resources on your back-end servers.

3. **Caching**: A reverse proxy server can cache responses from a server and serve these cached responses to clients. This reduces the load on the server and can significantly improve response times.

4. **Compression**: A reverse proxy can compress server responses before returning them to the client, which can significantly reduce transmission time.

5. **Serving Static Content**: Reverse proxies are often used to serve static content (like HTML pages, images, and videos) for a website. This can free up resources on the application server to handle dynamic content.

6. **Security and Anonymity**: By hiding the identity and characteristics of your back-end servers, a reverse proxy can protect your servers from direct attacks. It can also provide additional security features like SSL encryption and client authentication.

7. **Content Switching or URL Rewriting**: Based on the request, the reverse proxy can redirect to different servers. This can be used for A/B testing, gradual rollouts, and more.
---
#### What are some common use cases for forward proxy servers?

Forward proxy servers are commonly used in system design for several purposes:

1. **Access Control**: Forward proxies can be used to control access to certain websites or internet services within a network. This is often used in corporate or educational settings to block access to certain sites.

2. **Caching**: Forward proxies can cache responses from the internet and serve these cached responses to clients. This can reduce bandwidth usage and improve response times.

3. **Anonymity and Privacy**: By making requests on behalf of the client, a forward proxy can hide the client's IP address from the internet, providing anonymity. It can also be used to encrypt client requests, providing privacy.

4. **Geolocation Testing and Circumvention**: Forward proxies can be used to make requests from different geographical locations, which is useful for testing geolocation-specific behavior. They can also be used to circumvent geolocation restrictions.

5. **Bandwidth Savings**: By caching popular content, forward proxies can reduce the amount of data that needs to be fetched from the internet, saving bandwidth.

6. **Content Filtering**: Forward proxies can be used to filter and block certain types of content, such as ads or malicious websites.

7. **Load Balancing**: In some cases, forward proxies can also be used to distribute network traffic across multiple internet connections, improving bandwidth utilization and providing redundancy.


---
### Proxy in context of design patterns


In the context of design patterns in programming, a Proxy is a class functioning as an interface to something else. The proxy could interface to anything: a network connection, a large object in memory, a file, or some other resource that is expensive or impossible to duplicate. In short, a proxy is a wrapper or agent object that is being called by the client to access the real serving object behind the scenes.

Here's a simple example of a Proxy pattern in Java:

```java
interface Image {
    void display();
}

class RealImage implements Image {
    private String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadFromDisk();
    }

    private void loadFromDisk() {
        System.out.println("Loading " + filename);
    }

    @Override
    public void display() {
        System.out.println("Displaying " + filename);
    }
}

class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;

    public ProxyImage(String filename) {
        this.filename = filename;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(filename);
        }
        realImage.display();
    }
}

public class ProxyPatternDemo {
    public static void main(String[] args) {
        Image image = new ProxyImage("test_image.jpg");

        // Image will be loaded from disk
        image.display(); 
        System.out.println("");
        
        // Image will not be loaded from disk
        image.display(); 
    }
}
```

In this example, `ProxyImage` is a proxy class that reduces the memory footprint of `RealImage` until it's necessary to load and display the image. The `RealImage` class, which is a resource-intensive class, is only loaded and created when the `display` method is called.