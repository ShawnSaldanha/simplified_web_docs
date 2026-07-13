
Imagine you're logging into your online banking account.

You enter your username and password and click **Login**.

```text
Username: sujith@example.com
Password: MySecret@123
```

This information now needs to travel from your browser to the bank's server.

But here's an important question:

> **What prevents someone on the same Wi-Fi network from reading your password while it's travelling across the internet?**

The answer is **HTTPS**.

HTTPS ensures that communication between your browser and the server is encrypted, making it extremely difficult for anyone else to read or modify the transmitted data.

---

# What is HTTPS?

**HTTPS (HyperText Transfer Protocol Secure)** is the secure version of **HTTP**, the protocol used by browsers and servers to communicate.

The only difference is that HTTPS protects the communication using **SSL/TLS**, allowing data to travel securely over the internet.

Instead of sending information as plain text:

```text
Browser
    │
Username
Password
    │
Server
```

HTTPS encrypts the data before it leaves your browser.

```text
Browser
    │
Encrypted Data
    │
Server
```

Even if someone intercepts the communication, they will only see encrypted data rather than the original information.

---

# What are SSL and TLS?

You may have heard the terms **SSL** and **TLS** being used interchangeably.

- **SSL (Secure Sockets Layer)** was the original technology used to secure internet communication.
    
- **TLS (Transport Layer Security)** is the newer and more secure version that replaced SSL.
    

Today, almost every website actually uses **TLS**, but people still commonly refer to it as **SSL certificates** due to historical reasons.

So when someone says:

> "Install an SSL certificate"

they're usually referring to a TLS certificate.

---

# How HTTPS Works

Let's simplify the process.

### Step 1 — Browser Connects to the Website

Suppose you visit:

```text
https://example.com
```

The browser contacts the server.

---

### Step 2 — Server Proves Its Identity

The server sends its **digital certificate**.

This certificate contains information such as:

- Website name
    
- Public Key
    
- Certificate Authority (CA)
    
- Expiration date
    

Your browser checks whether this certificate was issued by a trusted authority.

If everything looks valid, the browser trusts that it is communicating with the genuine website.

---

### Step 3 — A Secure Connection is Established

Using the information exchanged during the handshake, the browser and server securely establish encryption keys.

Once this process is complete, all future communication becomes encrypted.

You don't need to understand the underlying mathematics at this stage—just remember that this initial exchange allows both sides to communicate securely for the rest of the session.

---

### Step 4 — Secure Communication

Now every request is encrypted before being transmitted.

```text
Browser
      │
Encrypted Request
      │
Internet
      │
Encrypted Response
      │
Server
```

Even though the data passes through many routers and networks across the internet, intermediate systems cannot read its contents.

---

# Why HTTPS is Important

HTTPS provides three major security benefits.

## 1. Encryption

All communication is encrypted.

Without HTTPS:

```text
Email
Password
Credit Card Number
```

could potentially be read if intercepted.

With HTTPS:

```text
Encrypted Data
```

is transmitted instead.

---

## 2. Authentication

HTTPS helps verify that you're actually communicating with the intended website.

For example,

```text
https://bank.com
```

instead of

```text
https://fake-bank.com
```

The browser verifies the website's certificate before establishing a secure connection.

---

## 3. Data Integrity

HTTPS also ensures that the transmitted data cannot be modified while travelling between the client and the server.

If someone attempts to alter the communication, the integrity checks will fail, and the connection will be rejected.

---

# HTTP vs HTTPS

|HTTP|HTTPS|
|---|---|
|Data is sent as plain text|Data is encrypted|
|No encryption|Uses TLS encryption|
|Less secure|Highly secure|
|Suitable only for non-sensitive communication|Recommended for all modern websites|
|Uses Port 80|Uses Port 443|

---

# The Lock Icon in Your Browser

When you visit a secure website, your browser usually displays a **lock icon** near the address bar.

This indicates that:

- the website is using HTTPS,
    
- the connection is encrypted,
    
- and the certificate has been verified by the browser.
    

However, remember:

> **The lock icon means the connection is secure—not necessarily that the website itself is trustworthy.**

A malicious website can also obtain a valid HTTPS certificate.

Always verify the website's domain before entering sensitive information.

---

# Does HTTPS Encrypt Everything?

Not exactly.

HTTPS encrypts the **contents** of the communication, such as:

- Usernames
    
- Passwords
    
- Form data
    
- API responses
    
- Images
    
- JSON data
    

However, some information remains visible so that the internet can route your request correctly, such as the destination IP address.

So HTTPS greatly improves privacy, but it doesn't make your internet activity completely invisible.

---

# The Big Picture

```text
Browser
      │
      │ Request
      ▼
TLS Handshake
      │
      ▼
Secure Connection Established
      │
      ▼
Encrypted Communication
      │
      ▼
Server
```

Every time you see **https://** in your browser, this secure communication process is happening behind the scenes before any sensitive data is exchanged.

---

# What's Next?

Now that communication between the browser and server is secure, another question arises:

> **Can any website on the internet send requests to my backend, or does the browser enforce restrictions?**

We'll answer that in the next topic:

➡️ [[CORS]]