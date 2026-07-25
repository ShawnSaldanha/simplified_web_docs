In the previous chapter, we learned how a request travels across the Internet using **DNS**, **routers**, and **NAT**.

Eventually, our request reaches the destination server.

But another question now comes up.

> **Once two devices find each other, how do they actually exchange data?**

For example,

- How does your browser communicate with Google's server?
    
- How does Netflix stream videos?
    
- How does an online game send your movements to the server?
    
- How does your Spring Boot application receive API requests?
    

Simply reaching the destination isn't enough.

The two devices also need a **set of rules** for exchanging data.

These rules are provided by the **Transport Layer**.

---

# What is the Transport Layer?

The Transport Layer is responsible for **communication between applications running on different devices**.

Its job is to make sure data reaches the correct application and, depending on the protocol being used, ensure that the communication is reliable.

Think of it like a courier company.

The Internet has already figured out **where** the parcel should go.

The Transport Layer now decides **how** the parcel should be delivered.

For example,

- Should the parcel require a signature before delivery?
    
- Should it be resent if it gets lost?
    
- Or should it simply be delivered as quickly as possible?
    

Different situations require different approaches.

That's why we have **TCP** and **UDP**.

---

# Why Do We Need Different Communication Methods?

Imagine you're sending different kinds of information.

Suppose you're sending:

- Bank transaction details
    
- A WhatsApp message
    
- A live football match
    
- Your position in an online game
    

Should all of them use the exact same communication method?

Probably not.

Some information **must never be lost**.

Other information is more important to receive **quickly**, even if a few pieces of data are missed.

That's why networking provides two main transport protocols.

- **TCP**
    
- **UDP**
    

---

# TCP (Transmission Control Protocol)

TCP focuses on one thing:

> **Reliability.**

Before sending any data, TCP first establishes a connection between the two devices.

Only after both sides agree does the communication begin.

This makes TCP reliable because it:

- Delivers data in the correct order.
    
- Detects missing data.
    
- Retransmits lost packets.
    
- Prevents duplicate data.
    

For applications where accuracy matters more than speed, TCP is the perfect choice.

Examples include:

- Web browsing (HTTP/HTTPS)
    
- Online banking
    
- Email
    
- File downloads
    
- Database communication
    

---

## The TCP Three-Way Handshake

Before communication begins, both devices first introduce themselves.

This process is called the **Three-Way Handshake**.

Think of it like making a phone call.

You don't immediately start talking.

Instead:

Person A:

> "Hello?"

Person B:

> "Hi, I can hear you."

Person A:

> "Great, let's begin."

Only then does the actual conversation start.

TCP works in almost the same way.

```text
Client
   │
   │  SYN
   ▼
Server
   ▲
   │ SYN + ACK
   │
Client
   │
   │ ACK
   ▼
Connection Established
```

The three steps are:

### Step 1 — SYN

The client asks:

> "Can we communicate?"

---

### Step 2 — SYN + ACK

The server replies:

> "Yes, I received your request and I'm ready."

---

### Step 3 — ACK

The client confirms:

> "Perfect. Let's start sending data."

Only after these three steps does the actual communication begin.

---

# Sequence Numbers

Imagine downloading a large movie.

The movie isn't sent as one giant piece.

Instead, it's divided into many smaller packets.

```text
Packet 1

Packet 2

Packet 3

Packet 4
```

Now imagine Packet 3 arrives before Packet 2.

How does the receiver know where each piece belongs?

That's why TCP uses **Sequence Numbers**.

Each packet receives a number that represents its position in the communication.

For example:

```text
Packet
Sequence Number

Packet A
100

Packet B
101

Packet C
102
```

Even if packets arrive out of order,

the receiver can rearrange them correctly using these numbers.

---

# Acknowledgements (ACK)

After receiving data,

the receiver sends back an **Acknowledgement (ACK)**.

This simply means:

> **"I successfully received your data."**

If the sender doesn't receive an acknowledgement within a certain amount of time,

it assumes the packet was lost and sends it again.

This is one of the main reasons TCP is considered reliable.

---

# UDP (User Datagram Protocol)

UDP takes a very different approach.

Instead of establishing a connection first,

it immediately starts sending data.

There is:

- No handshake.
    
- No acknowledgements.
    
- No retransmissions.
    
- No guarantee that packets arrive in order.
    

Because of this,

UDP is much faster than TCP.

---

# Why Would Anyone Use UDP?

At first, UDP sounds worse than TCP.

But consider a live football match.

If one video frame gets lost,

would you rather:

Wait for that missing frame to arrive...

or continue watching the match?

Most people would choose the second option.

Receiving the latest information is more important than perfectly receiving every packet.

That's why UDP is commonly used for:

- Live video streaming
    
- Video calls
    
- Online gaming
    
- Voice calls
    
- Live broadcasts
    

For these applications,

speed matters more than perfect accuracy.

---

# TCP vs UDP

|TCP|UDP|
|---|---|
|Connection-oriented|Connectionless|
|Reliable|Best effort|
|Uses acknowledgements|No acknowledgements|
|Guarantees packet order|Packet order is not guaranteed|
|Slower|Faster|
|Used for web browsing, banking, emails|Used for gaming, streaming, voice calls|

Neither protocol is "better."

They simply solve different problems.

---

# What are Ports?

So far we've learned that an IP address identifies a device.

But one device usually runs many applications.

For example,

your laptop might simultaneously have:

- Chrome
    
- Spotify
    
- Discord
    
- VS Code
    
- Spring Boot application
    

If data arrives at your laptop,

how does the operating system know **which application should receive it?**

That's where **Ports** come in.

---

## Why Do We Need Ports?

Think of an apartment building.

The street address identifies the building.

But once the delivery person reaches the building,

they still need the apartment number.

```text
Street Address
        │
        ▼
Apartment Building
        │
Apartment Number
```

Networking works similarly.

```text
IP Address
        │
Identifies Device
        │
        ▼
Port Number
        │
Identifies Application
```

The IP address gets the packet to the correct computer.

The **Port Number** delivers it to the correct application running on that computer.

---

## Common Port Numbers

Many services use well-known port numbers.

For example:

|Service|Default Port|
|---|--:|
|HTTP|80|
|HTTPS|443|
|FTP|21|
|SMTP|25|
|Spring Boot (default)|8080|

When we run our Spring Boot application locally,

we usually access:

```text
http://localhost:8080
```

Here,

- `localhost` identifies our own computer.
    
- `8080` identifies the Spring Boot application running on it.
    

Without ports,

your operating system wouldn't know which application should receive the request.

---

# Putting Everything Together

Let's follow a complete request.

Suppose we visit:

```text
https://example.com
```

```text
Browser
    │
DNS finds IP Address
    │
Router sends request
    │
Server receives packet
    │
TCP establishes connection
    │
Data sent to Port 443 (HTTPS)
    │
Server processes request
    │
Response sent back
    │
Browser displays webpage
```

Each layer has its own responsibility.

|Technology|Responsibility|
|---|---|
|IP Address|Find the correct device|
|Router|Forward packets across networks|
|TCP / UDP|Decide how data is exchanged|
|Port|Deliver data to the correct application|

Together, they make Internet communication possible.

---

# Key Takeaways

- The **Transport Layer** defines how applications communicate across a network.
    
- **TCP** prioritizes reliable and ordered communication.
    
- **UDP** prioritizes speed over reliability.
    
- TCP establishes communication using a **Three-Way Handshake**.
    
- **Sequence Numbers** keep packets in the correct order.
    
- **Acknowledgements (ACKs)** confirm successful delivery.
    
- **Ports** identify the specific application that should receive incoming data.
    
- Every network request is identified using both an **IP Address** and a **Port Number**.
    

---

# What's Next?

Now that we've learned how devices communicate and how applications exchange data, we're ready to look at the **common protocols** built on top of these networking concepts.

We'll explore protocols like **HTTP**, **HTTPS**, **FTP**, **SMTP**, **DHCP**, and **ICMP**, and understand the specific problem each one was designed to solve.

Continue to **[[Common Internet Protocols]]**.