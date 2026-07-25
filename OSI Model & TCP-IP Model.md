Throughout this Networking section, we've learned about many different technologies:

- IP Addresses
    
- MAC Addresses
    
- Ethernet
    
- Routers
    
- DNS
    
- NAT
    
- TCP
    
- UDP
    
- HTTP
    
- HTTPS
    
- Ports
    

At first, these may have felt like separate topics.

But in reality, they all work together whenever two devices communicate.

To make networking easier to understand and design, engineers organized these responsibilities into **layers**.

These layered architectures are called **network models**.

The two most well-known networking models are:

- **OSI Model**
    
- **TCP-IP Model**
    

Rather than introducing new technologies, these models simply organize everything we've already learned.

---

# Why Do We Need Networking Models?

Imagine building a car without dividing responsibilities.

One team would have to build:

- The engine
    
- The brakes
    
- The steering
    
- The seats
    
- The wheels
    
- The electronics
    

All at the same time.

That would quickly become difficult to manage.

Instead, car manufacturers divide the work into smaller parts, where each component has a specific responsibility.

Networking follows the same idea.

Instead of treating communication as one giant process, it's divided into layers.

Each layer performs one specific job and passes the data to the next layer.

```text
Application
      │
      ▼
Transport
      │
      ▼
Network
      │
      ▼
Physical Transmission
```

This layered approach makes networking easier to understand, develop, and troubleshoot.

---

# The OSI Model

The **OSI (Open Systems Interconnection) Model** is a conceptual model created to explain how network communication works.

It divides networking into **seven layers**, where each layer has a specific responsibility.

```text
┌──────────────────────────┐
│ 7. Application           │
├──────────────────────────┤
│ 6. Presentation          │
├──────────────────────────┤
│ 5. Session               │
├──────────────────────────┤
│ 4. Transport             │
├──────────────────────────┤
│ 3. Network               │
├──────────────────────────┤
│ 2. Data Link             │
├──────────────────────────┤
│ 1. Physical              │
└──────────────────────────┘
```

Let's briefly understand what each layer does.

---

## Layer 7 — Application

This is the layer closest to the user.

It's where application protocols like:

- HTTP
    
- HTTPS
    
- FTP
    
- SMTP
    
- DNS
    

operate.

Whenever your browser requests a webpage or your backend exposes a REST API, you're interacting with the Application Layer.

---

## Layer 6 — Presentation

This layer is responsible for how data is represented.

Typical responsibilities include:

- Encryption
    
- Compression
    
- Data formatting
    

For example,

when HTTPS encrypts your data using SSL/TLS, the Presentation Layer is involved.

---

## Layer 5 — Session

This layer manages communication sessions between applications.

It helps establish, maintain, and close conversations between two systems.

In modern web development, we rarely interact with this layer directly because many of its responsibilities are handled by application frameworks and protocols.

---

## Layer 4 — Transport

We've already studied this layer in detail.

Its responsibility is **end-to-end communication**.

Protocols here include:

- TCP
    
- UDP
    

It also uses **Port Numbers** to deliver data to the correct application.

---

## Layer 3 — Network

This layer is responsible for moving packets between different networks.

Technologies we've already learned here include:

- IP Addresses
    
- Routers
    
- Routing
    
- NAT
    

Its primary job is deciding **where packets should go**.

---

## Layer 2 — Data Link

This layer handles communication inside a local network.

Technologies we've already covered include:

- Ethernet
    
- MAC Addresses
    
- ARP
    

It ensures that data reaches the correct device within the same LAN.

---

## Layer 1 — Physical

The Physical Layer is responsible for actually transmitting data.

Examples include:

- Ethernet cables
    
- Wi-Fi signals
    
- Fiber optic cables
    

This is where electrical signals, radio waves, or light pulses physically travel from one device to another.

---

# The TCP-IP Model

Although the OSI Model is great for learning,

the Internet doesn't actually use all seven layers exactly as they are defined.

Instead, real-world networking is generally explained using the **TCP-IP Model**.

The TCP-IP Model combines some of the OSI layers, resulting in just **four layers**.

```text
┌──────────────────────────┐
│ Application             │
├──────────────────────────┤
│ Transport               │
├──────────────────────────┤
│ Internet                │
├──────────────────────────┤
│ Network Access          │
└──────────────────────────┘
```

This is the model you'll encounter most often when working with modern computer networks.

---

# OSI vs TCP-IP

The two models are very similar.

The main difference is that the TCP-IP Model combines several OSI layers together.

|OSI Model|TCP-IP Model|
|---|---|
|Application|Application|
|Presentation|Application|
|Session|Application|
|Transport|Transport|
|Network|Internet|
|Data Link|Network Access|
|Physical|Network Access|

You don't need to memorize this table.

The important thing to remember is:

- The **OSI Model** is mainly used for learning and understanding networking concepts.
    
- The **TCP-IP Model** is the model used by the Internet in practice.
    

---

# Where Does Everything We've Learned Fit?

Let's place all the technologies we've covered into these layers.

|Technology|OSI Layer|TCP-IP Layer|
|---|---|---|
|HTTP|Application|Application|
|HTTPS|Application|Application|
|DNS|Application|Application|
|FTP|Application|Application|
|SMTP|Application|Application|
|TCP|Transport|Transport|
|UDP|Transport|Transport|
|IP Address|Network|Internet|
|Routing|Network|Internet|
|NAT|Network|Internet|
|Ethernet|Data Link|Network Access|
|ARP|Data Link|Network Access|
|MAC Address|Data Link|Network Access|
|Wi-Fi / Ethernet Cable|Physical|Network Access|

Notice that nothing new has appeared here.

We've simply organized everything we've already learned into layers.

---

# Putting Everything Together

Let's follow one final request.

Suppose we open:

```text
https://www.google.com
```

The communication looks something like this:

```text
Browser
    │
HTTP/HTTPS creates the request
    │
TCP establishes a connection
    │
IP finds the destination network
    │
Ethernet sends data across the local network
    │
Wi-Fi carries the signals
    │
──────── Internet ────────
    │
Google Server
```

Every layer performs one job before passing the data to the next layer.

This layered approach is one of the biggest reasons the Internet is scalable and maintainable.

---

# Why Does This Matter for Backend Developers?

As backend developers, we don't usually implement networking protocols ourselves.

Frameworks like **Spring Boot**, **Node.js**, and **Express** handle most of the low-level networking details for us.

However, understanding these layers helps us answer questions like:

- Why is my API unreachable?
    
- Is the problem related to DNS?
    
- Is the TCP connection failing?
    
- Is Port 8080 open?
    
- Is the firewall blocking requests?
    
- Is HTTPS configured correctly?
    

Knowing where each technology fits makes debugging much easier.

---

# Key Takeaways

- Networking models divide communication into layers, each with a specific responsibility.
    
- The **OSI Model** has seven layers and is mainly used for learning and understanding networking concepts.
    
- The **TCP-IP Model** has four layers and is the model used by the Internet in practice.
    
- Technologies like HTTP, TCP, IP, and Ethernet each belong to different layers and work together to deliver data.
    
- Understanding these layers helps us better design, troubleshoot, and debug networked applications.
    

---

# Congratulations! 🎉

We've now completed the **Networking Concepts** section.

Starting from **how devices communicate**, we've explored:

- How networks are formed.
    
- How devices are identified using IP and MAC addresses.
    
- How data moves across local and global networks.
    
- How routers, DNS, and NAT guide requests across the Internet.
    
- How TCP and UDP transport data.
    
- How protocols like HTTP and HTTPS enable web communication.
    
- And finally, how all these technologies fit together in the **OSI** and **TCP-IP** models.
    

This networking knowledge forms a strong foundation for understanding backend development, microservices, cloud computing, and distributed systems.

---

# What's Next?

Now that we understand **how requests travel across networks**, we're ready to explore **how backend applications process those requests**.

Continue your backend journey with **[[Spring Framework]]**, where we'll learn how Java applications are structured and how frameworks like Spring simplify building modern backend systems.