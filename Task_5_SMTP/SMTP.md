# **Detailed Explanation of How SMTP (Simple Mail Transfer Protocol) Works**

SMTP is the standard protocol used for sending emails over the internet. It handles the delivery of messages from the sender's client to the recipient's mail server and between mail servers. SMTP operates on **port 25**, **port 465** (for SSL), and **port 587** (for TLS).

![How It Works](https://github.com/infans4/Tugas-Komunikasi-dan-Jaringan-Komputer-Pak-Fery/blob/main/Tugas-5_SMTP/assets/Cara-Kerja-SMTP.jpg)

###### Source: [Powercode Blog](https://blogs.powercode.id/mengenal-apa-itu-smtp-dan-cara-kerjanya/)

---

## **1. SMTP Architecture and Components**

SMTP operates in a **client-server** model, with the following key components:

### a. **Mail User Agent (MUA)**  
- The email client used by users to compose and send emails (e.g., Outlook, Thunderbird, Gmail).

### b. **Mail Transfer Agent (MTA)**  
- A server that receives emails from the MUA and forwards them to another MTA or MDA. It acts as an intermediary in email transmission.

### c. **Mail Delivery Agent (MDA)**  
- The component that receives emails from the MTA and stores them in the recipient's mailbox.

---

## **2. SMTP Workflow (Email Transmission Stages)**

### **Stage 1: Composing and Sending Email**  
- The user composes an email using an email client (MUA) and clicks "Send."  
- The MUA contacts the SMTP server to deliver the email.

### **Stage 2: Establishing Connection to the SMTP Server**  
- The MUA establishes a connection with the SMTP server using TCP/IP on the appropriate port (25, 465, or 587).  
- The SMTP server accepts the connection and initiates an SMTP session.

### **Stage 3: Email Transmission Process**  
Communication between the client and the SMTP server occurs via commands and responses:

1. **HELO/EHLO:**  
   The client introduces itself to the server.  
   Example:  
   ```bash
   HELO example.com
   ```

2. **MAIL FROM:**  
   The client specifies the sender's address.  
   Example:  
   ```bash
   MAIL FROM:<sender@example.com>
   ```

3. **RCPT TO:**  
   The client specifies the recipient's address.  
   Example:  
   ```bash
   RCPT TO:<recipient@example.com>
   ```

4. **DATA:**  
   The client sends the email content, including headers (subject, date, etc.) and the email body. The content is terminated with a single period (`.`) on an empty line.  
   Example:  
   ```bash
   DATA  
   Subject: Test Email  
   This is a test email.  
   .
   ```

5. **QUIT:**  
   Ends the session with the server.

### **Stage 4: Server-to-Server Email Transfer**  
- If the recipient's email domain is different, the SMTP server forwards the email to another MTA until it reaches the recipient's server.

### **Stage 5: Storage and Retrieval of Email**  
- Once the email reaches the recipient's server, it is stored by the MDA.  
- The recipient retrieves the email using protocols like POP3 or IMAP.

---

## **3. Protocols Related to SMTP**

- **POP3 (Post Office Protocol v3):**  
  Retrieves emails from the server and downloads them to the email client.

- **IMAP (Internet Message Access Protocol):**  
  Accesses emails directly on the server without downloading them.

---

## **4. Email Format in SMTP**

- **Header:** Contains metadata like the sender, recipient, subject, and other information.  
- **Body:** The main content of the email.

Example email header format:  
```text
From: sender@example.com  
To: recipient@example.com  
Subject: Sample Email  
Date: Wed, 28 Nov 2024 10:00:00 +0000  
```

---

## **5. SMTP Authentication and Security**

- **SMTP Authentication:**  
  Users must provide credentials (username and password) to send emails.

- **Encryption:**  
  - **STARTTLS:** Converts an unencrypted connection into an encrypted one.  
  - **SSL/TLS:** Establishes an encrypted connection from the start.

---

## **6. Common SMTP Issues and Solutions**

- **Relay Denied:**  
  The SMTP server refuses to relay emails due to improper relay settings.  
- **Authentication Failed:**  
  Incorrect or mismatched login credentials.  
- **Spam Filtering:**  
  Emails flagged as spam by the recipient's server.

---

## **7. Tools to Test SMTP**

- **Telnet:**  
  Tests connections to the SMTP server.  
  Example:  
  ```bash
  telnet smtp.example.com 25
  ```

- **OpenSSL:**  
  Tests SSL/TLS connections to the SMTP server.  
  Example:  
  ```bash
  openssl s_client -connect smtp.example.com:465
  ```

- **`swaks`:** A specialized tool for email testing.  
  Example:  
  ```bash
  swaks --to recipient@example.com --from sender@example.com --server smtp.example.com
  ```

---
