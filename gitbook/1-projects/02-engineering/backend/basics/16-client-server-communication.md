
## Standard HTTP Web Request
1. Client opens a connection and requests data from server.
2. Server calculates the response.
3. Server sends the response back to the client on the opened request.

## Ajax Polling
The client repeatedly polls (or requests) a server for data, and waits for the server to respond with data. If no data is available, an empty response is returned.

1. Client opens a connection and requests data from the server using regular HTTP.
2. The requested webpage sends requests to the server at regular intervals (e.g., 0.5 seconds).
3. The server calculates the response and sends it back, like regular HTTP traffic.
4. Client repeats the above three steps periodically to get updates from the server.

Problems
- Client has to keep asking the server for any new data.
- A lot of responses are empty, creating HTTP overhead.

## HTTP Long-Polling
The client requests information from the server exactly as in normal polling, but with the expectation that the server may not respond immediately.

1. The client makes an initial request using regular HTTP and then waits for a response.
2. The server delays its response until an update is available, or until a timeout has occurred.
3. When an update is available, the server sends a full response to the client.
4. The client typically sends a new long-poll request, either immediately upon receiving a response or after a pause to allow an acceptable latency period.

Each Long-Poll request has a timeout. The client has to reconnect periodically after the connection is closed, due to timeouts.

## WebSockets
- A persistent full duplex communication channels over a single TCP connection. Both server and client can send data at any time.
- A connection is established through WebSocket handshake.
- Low communication overhead.
- Real-time data transfer.

## Server-Sent Event (SSE)
1. Client requests data from a server using regular HTTP.
2. The requested webpage opens a connection to the server.
3. Server sends the data to the client whenever there’s new information available.

- Use case:
  - When real-time traffic from server to client is needed.
  - When server generates data in a loop and sends multiple events to client.

---
Server Client Communication protocols

Server-client communication is a fundamental concept in networking and is the basis for the internet. There are several methods for server-client communication, each with its own use cases and advantages. Here are some of the most common methods:

1. **HTTP/HTTPS**: This is the most common communication method on the internet. The client sends an HTTP request, and the server responds with an HTTP response. This is typically used for web browsing, REST APIs, etc.

2. **WebSockets**: This is a protocol that provides full-duplex communication channels over a single TCP connection. It is designed to be implemented in web browsers and web servers but can be used by any client or server application. It's useful for applications that require real-time communication between the server and the client.

3. **TCP/IP Sockets**: This is a low-level communication method that allows data to be sent directly over the internet. It's used for many different types of applications, including file transfers, email, and instant messaging.

4. **UDP**: Unlike TCP, UDP is connectionless. Clients do not need to establish a connection with the server before sending data. This makes UDP faster and more efficient, but less reliable. It's often used for live streaming and online gaming.

5. **gRPC**: This is a high-performance, open-source framework developed by Google. It uses HTTP/2 for transport, Protocol Buffers as the interface description language, and provides features such as authentication, load balancing, and more.

6. **RESTful APIs**: This is a set of constraints to be used for creating web services. Web services that conform to the REST architectural style, or RESTful web services, provide interoperability between computer systems on the internet.

7. **GraphQL**: This is a data query and manipulation language for APIs, and a runtime for executing those queries with your existing data. It provides an efficient and powerful alternative to REST.

8. **SOAP**: This is a messaging protocol specification for exchanging structured information in the implementation of web services in computer networks. It uses XML for its message format, and is widely used for web services and SOA-based projects.

Each of these methods has its own use cases, advantages, and disadvantages. The choice of which method to use depends on the specific requirements of the application.



---
Kotlin Implementation for Standard web request with HTTP

In Kotlin, you can use the `HttpURLConnection` class to make a regular HTTP web request. Here's a simple example of how to send a GET request:

```kotlin
import java.net.HttpURLConnection
import java.net.URL

fun sendGetRequest(url: String): String {
    val connection = URL(url).openConnection() as HttpURLConnection
    connection.requestMethod = "GET"

    val responseCode = connection.responseCode
    if (responseCode == HttpURLConnection.HTTP_OK) {
        return connection.inputStream.bufferedReader().use { it.readText() }  // defaults to UTF-8
    } else {
        throw RuntimeException("Failed : HTTP error code : $responseCode")
    }
}
```

You can call this function with the URL you want to send a request to:

```kotlin
val response = sendGetRequest("http://example.com")
println(response)
```

This code will send a GET request to the specified URL and print the response. If the server returns a status code other than 200 (HTTP_OK), it will throw a `RuntimeException`.


----

Web sockets 

To implement WebSocket communication in an Android application using Retrofit, you can use the OkHttp library, which is a dependency of Retrofit and supports WebSocket communication. Here's a simple example of how to do this:

First, add the OkHttp dependency to your `build.gradle` file:

```groovy
dependencies {
    implementation 'com.squareup.okhttp3:okhttp:4.9.3'
}
```

Next, create a WebSocket listener:

```kotlin
import okhttp3.Response
import okhttp3.WebSocket
import okhttp3.WebSocketListener
import okio.ByteString

class EchoWebSocketListener : WebSocketListener() {

    override fun onOpen(webSocket: WebSocket, response: Response) {
        webSocket.send("Hello, it's SSaurel !")
        webSocket.send("What's up ?")
        webSocket.send(ByteString.decodeHex("deadbeef"))
        webSocket.close(1000, "Goodbye, World!")
    }

    override fun onMessage(webSocket: WebSocket, text: String) {
        println("Receiving : $text")
    }

    override fun onMessage(webSocket: WebSocket, bytes: ByteString) {
        println("Receiving bytes : " + bytes.hex())
    }

    override fun onClosing(webSocket: WebSocket, code: Int, reason: String) {
        webSocket.close(1000, null)
        println("Closing : $code / $reason")
    }

    override fun onFailure(webSocket: WebSocket, t: Throwable, response: Response?) {
        t.printStackTrace()
    }
}
```

This listener sends a few messages to the server when the WebSocket connection is opened, and logs any messages it receives. It also handles failures and connection closures.

Finally, create a WebSocket connection using OkHttp:

```kotlin
import okhttp3.OkHttpClient
import okhttp3.Request

fun main() {
    val client = OkHttpClient()

    val request = Request.Builder().url("ws://echo.websocket.org").build()
    val listener = EchoWebSocketListener()

    val ws = client.newWebSocket(request, listener)

    // Trigger shutdown of the dispatcher's executor so this process can exit cleanly.
    client.dispatcher.executorService.shutdown()
}
```

This code creates a WebSocket connection to `ws://echo.websocket.org`, which is a public WebSocket server for testing. It uses the `EchoWebSocketListener` to handle messages.

Please note that this is a simple example and doesn't handle things like reconnection after failures or network changes. You'll need to handle these in a real-world application. Also, remember to replace the URL with your actual WebSocket server's URL.


----
#### WebRtc 

WebRTC (Web Real-Time Communication) is a free, open-source project that provides web browsers and mobile applications with real-time communication (RTC) via simple application programming interfaces (APIs). It allows audio and video communication to work inside web pages by allowing direct peer-to-peer communication, eliminating the need to install plugins or download native apps.

Supported by Google, Microsoft, Mozilla, and Opera, WebRTC is used in various apps for voice and video communication, including webpages, mobile apps, and IoT devices.

WebRTC includes several APIs:

- **MediaStream (getUserMedia)**: This API represents synchronized streams of media. For example, a stream taken from camera and microphone input has synchronized video and audio tracks.

- **RTCPeerConnection**: This API represents a WebRTC connection between the local computer and a remote peer. It provides methods to connect to a remote peer, maintain and monitor the connection, and close the connection once it's no longer needed.

- **RTCDataChannel**: This API represents a bidirectional data channel between two peers of a connection.

WebRTC is designed to work peer-to-peer, so users can connect by the most direct possible path, reducing latency and improving quality for real-time video communication.


---
TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are two of the most commonly used protocols in the transport layer of the TCP/IP model. They both send bits of data, known as packets, over the internet, but they do it in different ways.

**TCP**:
- TCP is a connection-oriented protocol, which means it establishes a connection before transmitting data.
- It provides reliable data transmission, ensuring that all packets arrive at their destination and in the correct order.
- It uses error checking and error recovery. If a packet is lost or corrupted, TCP will resend it.
- It controls the flow of data by adjusting the rate of data transmission based on network conditions.
- TCP is generally slower than UDP because of these additional features.
- It's used when reliability is more important than speed, such as in web browsing, email, file transfers, etc.

**UDP**:
- UDP is a connectionless protocol, which means it doesn't establish a connection before transmitting data.
- It provides unreliable data transmission. It doesn't guarantee that all packets will arrive or that they'll arrive in the correct order.
- It doesn't use error checking or error recovery. If a packet is lost or corrupted, UDP doesn't resend it.
- It doesn't control the flow of data, so it can transmit data as fast as desired.
- UDP is generally faster than TCP because it lacks these additional features.
- It's used when speed is more important than reliability, such as in live streaming, online gaming, VoIP, etc.

In summary, the choice between TCP and UDP depends on what you value more: reliability (TCP) or speed (UDP).

---
### how to use UDP in android directly with retrofit

Retrofit is a type-safe HTTP client for Android and Java, and it doesn't directly support TCP or UDP as it's built on top of OkHttp which is an HTTP+HTTP/2 client. However, you can use OkHttp for WebSocket (which works over TCP) communication as shown in the previous examples.  For UDP communication in Android, you would typically use the java.net.DatagramSocket and java.net.DatagramPacket classes.