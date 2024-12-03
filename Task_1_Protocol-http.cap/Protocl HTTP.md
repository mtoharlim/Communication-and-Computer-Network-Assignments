# Assignment 1: Protocol `http.cap`

This assignment explains the working mechanism of the HTTP protocol using the `http.cap` file.  

HTTP (HyperText Transfer Protocol) is a protocol used for transferring data on the web, enabling communication between clients (e.g., web browsers) and servers. The `http.cap` file is a network capture file containing HTTP data in packet form, which can be analyzed using tools like Wireshark. Below is a detailed explanation of how the HTTP protocol works and its technical aspects.

---

## Technical Aspects

- How HTTP Protocol and Socket Work  
- HTTP Headers  
- Number of Packets in HTTP Capture  
- Flow Graph of HTTP  

---

### 1. How HTTP Protocol and Socket Work

- **HTTP Basics**:  
  HTTP is a text-based protocol operating at the application layer of the OSI model. The client (browser) initiates a connection to the server using a TCP socket (usually port 80 for HTTP or port 443 for HTTPS).  

- **Socket Mechanism**:  
  The client opens a TCP socket to the server's IP address on the specified port, then sends an HTTP request. The TCP connection uses the three-way handshake mechanism: SYN, SYN-ACK, and ACK.  

- **Stateless Protocol**:  
  HTTP is stateless, meaning each client request is independent of previous ones. In HTTP/1.1, connections remain open for efficiency, while HTTP/2 and HTTP/3 provide advanced connection management and parallelism.

#### Screenshots:
![HTML Port](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Port%20HTML.png)  
![Socket](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Socket.png)  
![HTTP1.1](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/HTTP1.1.png)

---

### 2. HTTP Headers

HTTP headers contain essential information about requests and responses, divided into **Request Headers** and **Response Headers**.

- **Request Headers**: Sent by the client to provide details about the request. Examples:  
  - `GET /index.html HTTP/1.1`: Requests the resource `index.html`.  
  - `Host`: Specifies the domain name, e.g., `Host: www.example.com`.  
  - `User-Agent`: Identifies the client application or browser.  

- **Response Headers**: Sent by the server to indicate the status and provide metadata. Examples:  
  - `HTTP/1.1 200 OK`: Indicates a successful request.  
  - `Content-Type`: Specifies the type of content (e.g., `text/html` or `application/json`).  
  - `Content-Length`: Indicates the size of the content in the response.

#### Screenshots:
![HTTP GET](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/HTTP%20Get.png)  
![HTTP Response](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/HTTP%20Response.png)

---

### 3. Number of Packets in HTTP Capture

The number of packets sent during HTTP communication depends on the type and size of the request and response. Below are typical packets found in HTTP capture:

1. **Client-to-Server Request**:  
   - One packet to establish a TCP connection (three-way handshake).  
   - One packet for the HTTP request (e.g., `GET /index.html HTTP/1.1`).  

2. **Server-to-Client Response**:  
   - Status and header packet (e.g., `HTTP/1.1 200 OK`).  
   - Data packets containing the web page or file content.  

3. **Connection Closure**:  
   - For HTTP/1.0, the connection closes after the response.  
   - For HTTP/1.1 or newer, connections can remain open for multiple requests.

**Estimated Total Packets**:  
For a simple request (e.g., a `GET` with a small response), approximately 4–6 packets are involved, depending on content size.

#### Screenshots:  
![Client to Server](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Client%20to%20Server.png)  
![Server to Client](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Server%20to%20Client.png)  
![Close Connection](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Close%20conn.png)

---

### 4. HTTP Flow Graph in Wireshark

Wireshark's Flow Graph feature displays the communication flow between the client and server, including handshakes and HTTP packets. The flow graph typically includes:

1. **SYN, SYN-ACK, ACK**: Initiation of the TCP connection by the client.  
2. **HTTP GET**: The `GET` request from the client to the server.  
3. **HTTP 200 OK**: Response from the server indicating success.  
4. **Data Transfer**: Delivery of web page or file content from the server to the client.  
5. **Connection Closure**: TCP connection is closed if no further requests are made.

The file `http.cap` from the Wireshark Wiki can be downloaded and analyzed in Wireshark to see packet-level communication details.

#### Screenshots:  
![Flow 1](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Flow1.png)  


--- 
