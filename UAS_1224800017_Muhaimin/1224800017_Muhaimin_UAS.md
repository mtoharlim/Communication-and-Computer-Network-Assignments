# Answers for TCP Segments in Wireshark Analysis  

### **1. Source IP Address and Port Number**  
- **IP Address (Source):** `192.168.9.98` (Local Host)  
- **Port Number (Source):** `50768`  

These details indicate that the client machine initiates the connection from IP `192.168.9.98` using port `50768`.

---

### **2. Destination IP Address and Port Number Used by gaia.cs.umass.edu**  
- **Destination IP Address:** `128.119.245.12`  
  - Identifies the server’s NIC configured to receive network traffic.  
- **Destination Port Number:** `80`  
  - Indicates that the client communicates with the server using HTTP.  

**Screenshot Evidence:**  
Please filter the Wireshark capture with `ip.src == 192.168.9.98 && ip.dst == 128.119.245.12`.

---

### **3. Sequence Number and SYN Segment Identification**  
- **Sequence Number (SYN Segment):** `0`  
  - This is the initial sequence number sent by the client during the TCP three-way handshake.  
- **Identification of SYN Segment:**  
  - The SYN flag is set in the TCP header (`0x002`).  
  - No acknowledgment number is present, as it’s the connection initiation step.  

**Screenshot Evidence:**  
Filter with `tcp.flags.syn == 1 && ip.src == 192.168.9.98`.

---

### **4. SYNACK Segment Details**  
- **Sequence Number (SYNACK):** `0`  
- **Acknowledgment Number:** `1`  
  - The server acknowledges the client’s SYN by adding 1 to the initial sequence number (`0`).  
- **Identification of SYNACK Segment:**  
  - Both SYN and ACK flags are set in the TCP header.  

**Screenshot Evidence:**  
Filter with `tcp.flags.syn == 1 && tcp.flags.ack == 1`.

---

### **5. Sequence Number of TCP Segment Containing HTTP POST**  
- **Sequence Number:** `152984`  
  - This can be found in the "Sequence Number" field of the TCP segment containing the "POST" command in its data field.  

**Steps to Find:**  
1. Use Wireshark’s display filter:  
   ```  
   http.request.method == POST  
   ```  
2. Inspect the packet details to locate the sequence number.

---

### **6. Sequence Numbers, RTTs, and EstimatedRTTs for First Six Segments**  

#### Sequence Numbers and ACK Information:  
- **Segments 1-6:** Nos. `714`, `715`, `716`, `717`, `718`, `719`  
- **ACKs for Segments 1-6:** Nos. `929`, `930`, `931`, `932`, `933`, `934`  

#### RTT and EstimatedRTT Calculation:  
Using the formula:  
\[ \text{EstimatedRTT} = 0.875 \times \text{EstimatedRTT} + 0.125 \times \text{SampleRTT} \]  

| **Segment** | **Sent Time (s)** | **ACK Received Time (s)** | **SampleRTT (s)** | **EstimatedRTT (s)** |  
|-------------|-------------------|---------------------------|-------------------|-----------------------|  
| 714         | 9.522558          | 11.064822                 | 1.542264          | 1.542264              |  
| 715         | 9.529228          | 11.065782                 | 1.536554          | 1.541617              |  
| 716         | 9.529228          | 11.066192                 | 1.536964          | 1.540995              |  
| 717         | 10.176342         | 11.067192                 | 0.890850          | 1.460584              |  
| 718         | 10.176342         | 11.067592                 | 0.891250          | 1.398591              |  
| 719         | 10.176342         | 11.067992                 | 0.891650          | 1.333048              |  

#### Observing RTT:  
Wireshark’s `TCP Stream Graph` → `Round Trip Time Graph` provides visual RTT information.

---

### **7. Lengths of the First Six TCP Segments**  
- **HTTP POST Segment:** `663 bytes`  
- **Other Five Segments:** `1460 bytes each`  
  - This value represents the Maximum Segment Size (MSS) for these packets.  

**Steps to Find:**  
1. Filter for TCP packets in Wireshark using the source and destination IP.  
2. Look at the "Length" field in the packet details pane.  

---