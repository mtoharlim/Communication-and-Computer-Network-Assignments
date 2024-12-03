# Assignment 2: Socket Protocol

This assignment focuses on explaining the workings of socket protocols.

The task references a simple socket programming example using the terminal, available at the following link:  
[GitHub: Simple Server and Client Socket Programming](https://github.com/kusdavletov/socket-programming-simple-server-and-client/blob/master/README.md).  

The discussion covers the following topics:

---

## **Technical Aspects**

1. **How Socket Protocols Work**  
2. **Number of Packets in the Capture**  
3. **Flow Graph**  

---

### **1. How Socket Protocols Work**

- **Socket:** The client opens a TCP socket to the server's IP address on a specified port and sends a connection request. The TCP connection is established using a **three-way handshake**: SYN, SYN-ACK, and ACK to initiate communication.

#### **Screenshot**
![3WayHandShake](https://github.com/infans4/Tugas-2_Penjelasan-Protokol-Socket/blob/main/assets/3HandShake.png)

---

### **2. Number of Packets in the Capture**

The number of packets exchanged in communication depends on the type and size of the request and response. Here are some examples:

- **Client-to-Server Request:**  
   A single packet is sent to open the TCP connection (**three-way handshake**).  
- **Server-to-Client Response:**  
   Data packets containing the requested content or file.  
- **Closing the Connection:**  
   The connection is closed once the response is complete.  

For a basic request (e.g., a simple `GET` request with a small response), the total packet count typically ranges from **4-6 packets**, depending on the content size.

#### **Screenshots**
![3WayHandShake](https://github.com/infans4/Tugas-2_Penjelasan-Protokol-Socket/blob/main/assets/3HandShake.png)  
![SendClient](https://github.com/infans4/Tugas-2_Penjelasan-Protokol-Socket/blob/main/assets/SendClientnServer.png)  
![ClientOut](https://github.com/infans4/Tugas-2_Penjelasan-Protokol-Socket/blob/main/assets/ClientOut.png)  

---

### **3. Flow Graph in Wireshark**

Wireshark's **Flow Graph** feature provides a visual representation of the communication between the client and server. It highlights the following steps:

1. **SYN, SYN-ACK, ACK:** The client initiates the TCP connection.  
2. **Data Transfer:** The server sends the requested data to the client.  
3. **Connection Closure:** If no further requests are made, the TCP connection is terminated.  

#### **Screenshot**
![FlowGraph](https://github.com/infans4/Tugas-2_Penjelasan-Protokol-Socket/blob/main/assets/FlowGraph.png)  

--- 
