So far, we've learned:

- How devices communicate with each other.
    
- How IP addresses identify devices.
    
- How routers move data across networks.
    
- How TCP and UDP transport data.
    
- How ports deliver data to the correct application.
    

But one question still remains.

> **What exactly is the data being exchanged?**

When you browse a website, send an email, or upload a file, your computer isn't inventing its own way of communicating.

Instead, it follows a predefined set of rules called **protocols**.

Different tasks require different protocols.

For example:

- Browsing a website uses one protocol.
    
- Sending an email uses another.
    
- Uploading files uses another.
    
- Automatically obtaining an IP address uses another.
    

Let's look at some of the most common Internet protocols you'll encounter as a developer.

---

# HTTP (HyperText Transfer Protocol)

Whenever you visit a website, your browser needs a way to request web pages from a server.

That's exactly what **HTTP** was designed for.

Imagine you're sitting in a restaurant.

You place an order.

The waiter carries your order to the kitchen.

The kitchen prepares your food.

The waiter brings it back.

HTTP works in a very similar way.

```text
Browser
    │
HTTP Request
    ▼
Server
    │
Processes Request
    ▼
HTTP Response
    │
Browser displays webpage
```

Your browser sends an **HTTP Request**.

The server processes it.

The server sends back an **HTTP Response**.

Almost every website you visit works this way.

---

## HTTP is Stateless

One important characteristic of HTTP is that it's **stateless**.

This simply means that every request is treated independently.

Imagine ordering food from a waiter who completely forgets you after every order.

Each time you want something, you have to introduce yourself again.

That's essentially how HTTP works.

Every request contains all the information the server needs to process it.

If websites need to remember users (for example, keeping someone logged in), they use mechanisms like **sessions** or **JWTs**, which we covered in the **Security Foundations** section.

---

# HTTPS (HTTP Secure)

HTTP works well.

But there's one major problem.

By itself, HTTP doesn't encrypt the data being transmitted.

That means someone intercepting the communication could potentially read the information being exchanged.

That's where **HTTPS** comes in.

HTTPS is simply:

> **HTTP + SSL/TLS Encryption**

Instead of sending plain text,

the data is encrypted before it travels across the network.

```text
Browser
    │
Encrypted Data
    ▼
Server
```

This protects sensitive information such as:

- Passwords
    
- Credit card details
    
- Banking information
    
- Personal data
    

Whenever you see the small lock icon in your browser's address bar, you're using HTTPS.

---

# FTP (File Transfer Protocol)

Sometimes we don't want to browse a website.

We simply want to transfer files between two computers.

That's the purpose of **FTP**.

FTP allows files to be:

- Uploaded
    
- Downloaded
    
- Managed
    

between a client and a server.

For example:

```text
Your Laptop
      │
 Upload File
      ▼
FTP Server
```

Although cloud storage services have become more common today, FTP is still used in many organizations for file transfers and server management.

---

# SMTP (Simple Mail Transfer Protocol)

Whenever you send an email,

your email application doesn't directly contact the recipient.

Instead,

it sends the email to a mail server using **SMTP**.

```text
Your Email App
       │
SMTP
       ▼
Mail Server
       │
Recipient's Mail Server
```

SMTP's responsibility is **sending emails**.

Receiving emails is handled by other protocols, such as IMAP or POP3, but those are outside the scope of this guide.

As backend developers, you'll commonly use SMTP when building features like:

- Email verification
    
- Password reset emails
    
- Notification emails
    

---

# DHCP (Dynamic Host Configuration Protocol)

Earlier, we learned that every device needs an IP address.

But imagine manually assigning an IP address every time a new device connects to Wi-Fi.

That would quickly become frustrating.

Instead, this process is automated using **DHCP**.

Whenever you connect a new device to a network,

it asks:

> **"Can someone give me an IP address?"**

The DHCP server responds by assigning one automatically.

```text
Laptop Joins Wi-Fi
        │
        ▼
Requests IP Address
        │
        ▼
DHCP Server
        │
Assigns IP Address
        ▼
Laptop is Ready
```

Most home routers include a built-in DHCP server, which is why you rarely have to configure IP addresses manually.

---

# ICMP (Internet Control Message Protocol)

Unlike HTTP or SMTP,

**ICMP** isn't used to transfer application data.

Instead,

it's used to report network information and diagnose connectivity problems.

One of the most common examples is the **ping** command.

When you run:

```bash
ping google.com
```

your computer sends an ICMP request.

If Google responds,

you know the destination is reachable.

```text
Your Computer
      │
ICMP Echo Request
      ▼
Server
      │
ICMP Echo Reply
      ▼
Your Computer
```

Network administrators often use ICMP to troubleshoot network issues.

---

# Which Protocol Uses Which Transport Protocol?

Earlier, we learned about **TCP** and **UDP**.

The protocols we've just discussed are built on top of them.

|Protocol|Uses|
|---|---|
|HTTP|TCP|
|HTTPS|TCP|
|FTP|TCP|
|SMTP|TCP|
|DHCP|UDP|
|ICMP|Neither TCP nor UDP (works directly over IP)|

Notice that most application protocols rely on **TCP** because they need reliable communication.

DHCP uses UDP because it's designed to be lightweight and fast.

ICMP is a special protocol used for diagnostics, so it doesn't rely on either TCP or UDP.

---

# Putting Everything Together

Let's follow what happens when we open a secure website.

```text
Browser
    │
DNS finds server's IP
    │
TCP establishes connection
    │
HTTPS Request
    │
Server processes request
    │
HTTPS Response
    │
Browser displays webpage
```

Each protocol has its own responsibility.

|Protocol|Responsibility|
|---|---|
|HTTP|Transfer web pages and API requests|
|HTTPS|Secure web communication|
|FTP|Transfer files|
|SMTP|Send emails|
|DHCP|Automatically assign IP addresses|
|ICMP|Test connectivity and report network issues|

Together, these protocols allow the Internet to support everything from web browsing and email to file sharing and network management.

---

# Key Takeaways

- A **protocol** is a set of rules that defines how devices communicate for a specific purpose.
    
- **HTTP** is used to transfer web pages and API requests.
    
- **HTTPS** secures HTTP communication using SSL/TLS encryption.
    
- **FTP** is designed for transferring files.
    
- **SMTP** is used to send emails.
    
- **DHCP** automatically assigns IP addresses to devices joining a network.
    
- **ICMP** is used for network diagnostics and tools like `ping`.
    
- Most application protocols rely on **TCP**, while DHCP uses **UDP**, and ICMP operates directly over IP.
    

---

# What's Next?

Congratulations! 🎉

You've now built a solid understanding of how data travels across networks—from identifying devices with IP addresses to routing packets across the Internet and using protocols like HTTP and HTTPS to exchange information.

The next chapter, **[[OSI Model & TCP-IP Model]]**, ties everything together by showing **where each networking concept fits into the overall architecture**. Instead of learning new technologies, we'll organize everything we've already learned into two widely used networking models, making it much easier to understand how all the pieces work together.