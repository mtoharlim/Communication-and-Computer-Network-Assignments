# Assignment 3: HTTP Protocols

This assignment explains the workings of HTTP/1.1, HTTP/2.0, and HTTP/3.0 protocols.

---

## **Technical Aspects**

1. Advantages of Each HTTP Protocol  
2. How Each Protocol Works  
3. Flow Graph of Each Protocol  

---

## **HTTP 1.1**

### **Advantages of HTTP 1.1**

1. **Persistent Connections (Keep-Alive):**  
   HTTP 1.1 allows connections to stay open for multiple requests, reducing the overhead of reopening connections compared to HTTP 1.0.  
2. **Chunked Transfer Encoding:**  
   The server can start sending data before the entire response is processed, improving efficiency for dynamic content delivery.  
3. **Host Header Support:**  
   HTTP 1.1 uses the `Host` header to enable virtual hosting, allowing multiple domains to share one IP address.  
4. **Pipelining:**  
   HTTP 1.1 supports sending multiple requests without waiting for the previous response to complete (though rarely used due to client-side implementation limitations).  
5. **Improved Caching:**  
   Introduced headers like `Cache-Control` and `ETag` for better caching management.  

---

### **How HTTP 1.1 Works**

#### **Communication Process:**

1. The **client** (e.g., browser) opens a connection to the server using TCP/IP.  
2. The client sends an HTTP request, including the method (GET, POST), URL, and headers.  
3. The **server** processes the request and responds with an HTTP response containing headers (e.g., status, content type) and body (e.g., HTML or JSON).  
4. If `Keep-Alive` is enabled, the connection remains open for subsequent requests, reducing the need to reopen it.  

#### **Key Features:**

- The `Host` header is mandatory to support multiple domains on one server.  
- Persistent connections reduce delays for frequent requests.  

#### **Screenshot**
![HTTP1.1](https://github.com/infans4/Tugas-3_HTTP-1.1/blob/main/assets/HTTP1.1.png)  

---

### **Flow Graph in Wireshark**

Wireshark's Flow Graph feature displays the communication flow between client and server, including handshakes and packets sent. The steps shown include:  

1. **SYN, SYN-ACK, ACK:** The client initiates the TCP connection.  
2. **Data Transfer:** Content data is sent from the server to the client.  
3. **Connection Closure:** The TCP connection is closed if no further requests are made.  

#### **Screenshot**
![FlowGraph](https://github.com/infans4/Tugas-3_HTTP-1.1/blob/main/assets/HTTP1.1Flow.png)  

---

## **HTTP 2.0**

### **Advantages of HTTP 2.0**

1. **Multiplexing:**  
   Allows multiple requests to be sent over a single TCP connection without blocking, solving HTTP/1.1's head-of-line blocking issue.  
2. **Header Compression:**  
   Reduces data size by compressing headers using the HPACK algorithm.  
3. **Binary Protocol:**  
   Faster processing with binary protocol instead of text-based communication.  
4. **Prioritization:**  
   Allows prioritizing specific requests, ensuring critical resources (e.g., CSS, JavaScript) are loaded faster.  
5. **Server Push:**  
   Servers can send data preemptively (e.g., CSS/JS files) before being requested by the client, reducing latency.  

---

### **How HTTP 2.0 Works**

1. **HTTPS Connection:**  
   HTTP/2 operates over TLS, ensuring encrypted and secure data transmission.  
2. **Streams:**  
   - A single connection consists of multiple independent streams.  
   - Data is sent as smaller *frames*, which are reassembled by the client.  
3. **Header Compression:**  
   Frequently used headers (e.g., `User-Agent`, `Host`) are compressed for efficiency.  
4. **Server Push:**  
   Servers analyze client requests and preemptively send related resources (e.g., CSS, JS files).  

#### **Screenshot**
![HTTP2.0](https://github.com/infans4/Tugas-3_HTTP-1.1/blob/main/assets/HTTP2.0.png)  

---

### **Flow Graph in Wireshark**

Wireshark's Flow Graph for HTTP/2 shows a similar process to HTTP/1.1 but highlights HTTP/2 features such as multiplexed streams.  

1. **SYN, SYN-ACK, ACK:** The client initiates the TCP connection.  
2. **Data Transfer:** Data frames are sent between the server and the client.  
3. **Connection Closure:** The TCP connection is closed if no further requests are made.  

#### **Screenshot**
![FlowGraph](https://github.com/infans4/Tugas-3_HTTP-1.1/blob/main/assets/HTTP2.0Flow.png)  

--- 
