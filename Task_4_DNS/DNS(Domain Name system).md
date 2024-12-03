# **Detailed Explanation of How DNS (Domain Name System) Works**

The Domain Name System (DNS) is a distributed system that allows devices on a network, such as the internet, to translate domain names into IP addresses. Computers do not understand domain names like `www.google.com`; instead, they rely on IP addresses to locate the correct server.

![How It Works](https://github.com/infans4/Tugas-Komunikasi-dan-Jaringan-Komputer-Pak-Fery/blob/main/Tugas-4_DNS/assets/DNS-Query.jpeg)

###### Source: [Cloud Raya Blog](https://cloudraya.com/blog/apa-itu-dns/)

---

## **1. DNS Structure and Components**

DNS is designed as an inverted tree hierarchy with several levels, each playing a specific role:

### a. **Root DNS Servers**  
- The root server is the starting point in the DNS query process.  
- There are only 13 sets of **root servers** (labeled A to M), but each has multiple copies worldwide for redundancy.  

### b. **Top-Level Domain (TLD) Servers**  
- TLD servers are responsible for top-level domains like `.com`, `.org`, `.net`, or country-specific domains like `.id` (Indonesia).  

### c. **Authoritative Name Servers**  
- These servers store complete DNS information for a specific domain. For example, the authoritative server for `example.com` contains all DNS records related to that domain.  

### d. **Recursive Resolver (DNS Resolver)**  
- The client (e.g., a computer or router) initiates the DNS request and relies on the resolver to find DNS information.  

---

## **2. DNS Resolution Steps (Domain Name Translation Process)**

When you type a domain like `www.example.com` in your browser:

1. **DNS Request Sent by the Client**  
   The computer sends a DNS request to the resolver, often provided by the ISP or DNS services like Google (8.8.8.8) or Cloudflare (1.1.1.1).  

2. **Local Cache Check**  
   The resolver checks its cache for the result. If it exists and is valid (within the TTL period), the resolver immediately returns the IP address.  

3. **Querying the Root DNS Server**  
   If no cached result is found, the resolver queries the **Root DNS Server**, which does not provide the IP address but directs the resolver to the appropriate **TLD Server**.  

4. **Querying the TLD Server**  
   The resolver contacts the TLD server for the domain, such as `.com`, which directs the resolver to the **Authoritative Name Server**.  

5. **Querying the Authoritative Name Server**  
   The resolver queries the authoritative server for the domain, which provides the actual IP address of the requested domain.  

6. **Returning the IP Address to the Client**  
   The resolver returns the IP address to the client computer, which uses it to communicate with the target server.  

7. **Connecting to the Target Server**  
   The browser establishes an HTTP/HTTPS connection to the server using the obtained IP address.  

---

## **3. Types of DNS Records**

DNS uses various record types, each serving a specific purpose:

- **A Record:** Maps a domain name to an IPv4 address.  
- **AAAA Record:** Maps a domain name to an IPv6 address.  
- **CNAME Record:** An alias that points to the main domain.  
- **MX Record:** Specifies the mail server for a domain.  
- **TXT Record:** Stores text data, often used for domain ownership verification or security configurations like SPF and DKIM.  
- **NS Record:** Specifies the authoritative name servers for a domain.  
- **PTR Record:** Provides reverse DNS lookup, mapping IP addresses to domain names.  

---

## **4. Cache and TTL (Time To Live)**

- **Cache:**  
  Both resolvers and computers temporarily store DNS query results to speed up future lookups.  
- **TTL:**  
  Each DNS record has a TTL value, defining how long the record is valid before it needs to be refreshed from the DNS server.  

---

## **5. DNS Query Modes: Recursive vs. Iterative**

- **Recursive Query:**  
  The resolver performs the entire query process (from root to authoritative server) and returns the final result to the client.  

- **Iterative Query:**  
  The resolver provides partial results, directing the client to the next server in the hierarchy.  

---

## **6. DNS Security and Modern Protocols**

- **DNSSEC (DNS Security Extensions):**  
  Provides digital signatures to ensure DNS records are not tampered with during transmission.  

- **DNS over HTTPS (DoH):**  
  Encrypts DNS queries using HTTPS, enhancing privacy and security.  

- **DNS over TLS (DoT):**  
  Uses TLS to encrypt DNS traffic, adding an extra layer of security.  

---

## **7. Practical Example**

Suppose you want to access `www.example.com`:  

1. **Step 1:**  
   The client sends a DNS request to the resolver.  

2. **Step 2:**  
   The resolver checks its local cache. If no cached result is found, it queries the root server.  

3. **Step 3:**  
   The root server directs the resolver to the `.com` TLD server.  

4. **Step 4:**  
   The TLD server directs the resolver to the authoritative server for `example.com`.  

5. **Step 5:**  
   The resolver retrieves the IP address from the authoritative server and returns it to the client.  

---

## **8. Tools for DNS Analysis**

- **`nslookup` (Command Line):**  
  A simple tool for checking DNS information.  
  Example:  
  ```bash
  nslookup www.google.com
  ```  

- **`dig` (Command Line):**  
  A more advanced tool for DNS analysis.  
  Example:  
  ```bash
  dig example.com +trace
  ```  

---
