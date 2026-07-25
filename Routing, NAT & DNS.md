In the previous chapter, we learned how devices communicate **within the same local network** using MAC addresses, Ethernet, and ARP.

But what if the device we're trying to reach isn't connected to our Wi-Fi?

For example, when you visit:

```text
https://www.google.com
```

Google's servers certainly aren't sitting inside your home.

They could be hundreds or even thousands of kilometers away.

So how does your request know where to go?

This is where **Routing**, **DNS**, and **NAT** work together.

---

## The Journey of a Request

Let's first look at the complete journey.

We'll understand each step in detail afterward.

```text
Browser
    │
    ▼
DNS finds the server's IP Address
    │
    ▼
Router forwards the request
    │
    ▼
Internet
    │
    ▼
Google Server
    │
    ▼
Response comes back
```

Although this entire process usually takes only a few milliseconds, several networking technologies work together behind the scenes.

---

# What is Routing?

Imagine you want to send a parcel from Bangalore to New York.

The parcel doesn't magically appear there.

Instead, it travels through several distribution centers before reaching its destination.

The Internet works in a similar way.

Data doesn't travel directly from your laptop to the destination server.

Instead, it passes through multiple devices called **routers**.

Each router makes one simple decision:

> **"Which path should I send this packet through next?"**

That's exactly what **Routing** is.

It is the process of choosing the best path for data to travel from one network to another.

---

## Why Do We Need Routers?

Inside your home, all your devices belong to the same local network.

```text
Laptop
Phone
TV
Printer
```

Communicating inside this network is relatively simple.

But what if your laptop wants to reach Google's servers?

Google belongs to an entirely different network.

Something has to connect these two different networks together.

That's the router's job.

```text
Your Laptop
      │
      ▼
Home Router
      │
      ▼
Internet
      │
      ▼
Google Server
```

You can think of a router as a traffic officer.

Every time data arrives, it checks:

> "Where should this packet go next?"

It doesn't know the entire journey.

It only knows the **next best direction**.

The next router repeats the same process.

Eventually, the packet reaches its destination.

---

# What is DNS?

Now another question arises.

When we type:

```text
google.com
```

how does the router know where Google is?

The answer is...

It doesn't.

Routers don't understand website names.

They only understand **IP addresses**.

So before our request can even begin its journey, we first need to convert the website name into an IP address.

That's the job of **DNS (Domain Name System).**

---

## Why Do We Need DNS?

Imagine if every contact in your phone was stored only as phone numbers.

Instead of calling:

> Mom

you'd have to remember

```text
+91-9876543210
```

for every person.

That would be impossible.

Instead, your phone stores names while internally keeping track of the phone numbers.

DNS works exactly the same way.

```text
We remember

google.com
```

↓

```text
DNS translates it into

142.xxx.xxx.xxx
```

↓

```text
Computer sends the request
```

Without DNS, we'd have to memorize IP addresses for every website we visit.

---

## How DNS Works

Suppose we type:

```text
https://www.google.com
```

The browser first asks:

> "What is the IP address of google.com?"

The DNS server replies:

```text
google.com

↓

142.xxx.xxx.xxx
```

Now the browser finally knows where to send the request.

A simplified flow looks like this.

```text
Browser
    │
    ▼
DNS Server
    │
Returns Google's IP
    │
    ▼
Browser sends request
```

Notice that DNS only helps us **find the server**.

It doesn't actually send our request.

That job belongs to routers.

---

# Public and Private Networks

Earlier, we learned that devices inside your home use **Private IP Addresses**.

For example,

```text
Laptop

192.168.1.10
```

Phone

```text
192.168.1.11
```

These addresses only exist inside your home network.

The rest of the Internet cannot directly see them.

So another question appears.

If Google cannot see my private IP address...

How does Google send a response back?

The answer is **NAT**.

---

# What is NAT?

**NAT (Network Address Translation)** allows many devices inside a private network to share a single public IP address.

Imagine four devices connected to your home Wi-Fi.

```text
Laptop

192.168.1.10

Phone

192.168.1.11

TV

192.168.1.12

Tablet

192.168.1.13
```

Your ISP usually gives your home **only one Public IP Address**.

```text
49.xxx.xxx.xxx
```

So before your request leaves your house,

the router replaces your private IP with the public IP.

```text
Laptop

192.168.1.10
        │
        ▼
Home Router
        │
Changes Address
        ▼
49.xxx.xxx.xxx
        │
        ▼
Internet
```

Now Google only sees your home's public IP address.

---

## Why Do We Need NAT?

Imagine every phone, laptop, TV, smartwatch, refrigerator, and gaming console needed its own public IP.

We would quickly run out of addresses.

Instead,

NAT allows hundreds of devices to safely share a single public IP.

It also adds a small layer of security because devices on the Internet cannot directly see your private network.

---

# What is PAT?

You might now wonder:

> **If every device shares the same public IP, how does the router know which response belongs to which device?**

For example,

both your laptop and phone might open Google at the same time.

They both leave your house using the same public IP.

How does the router avoid mixing up the responses?

This is solved by **PAT (Port Address Translation).**

Instead of tracking devices using only IP addresses,

the router also keeps track of **port numbers**.

```text
Public IP

49.xxx.xxx.xxx

↓

Laptop

Port 5001

↓

Phone

Port 5002
```

When Google's response comes back,

the router checks the port number and forwards the response to the correct device.

We'll understand ports in much greater detail in the next chapter.

---

# Putting Everything Together

Let's follow the complete journey one last time.

Suppose we open:

```text
https://www.google.com
```

```text
Browser
    │
    ▼
DNS finds Google's IP Address
    │
    ▼
Router receives the request
    │
    ▼
NAT replaces the private IP
with the public IP
    │
    ▼
Internet
    │
    ▼
Google Server
    │
Processes Request
    │
    ▼
Response travels back
    │
    ▼
Router uses PAT to identify
the correct device
    │
    ▼
Browser displays the webpage
```

Although this entire journey happens in just a few milliseconds, multiple networking technologies work together seamlessly to make it possible.

---

# Key Takeaways

- **Routing** is the process of moving data between different networks.
    
- **Routers** decide the next best path for packets traveling across the Internet.
    
- **DNS** translates human-readable domain names into IP addresses.
    
- **Private IP Addresses** are used within local networks, while **Public IP Addresses** identify networks on the Internet.
    
- **NAT** allows multiple devices to share a single public IP address.
    
- **PAT** uses port numbers to ensure responses are delivered to the correct device when many devices share the same public IP.
    

---

# What's Next?

So far, we've learned **where** data travels and **how** it reaches the correct destination.

The next question is:

> **Once two devices find each other, how do they reliably exchange data?**

To answer that, we'll explore **TCP**, **UDP**, **ports**, and the **TCP three-way handshake**, which form the foundation of communication between applications.

Continue to **[[Transport Layer (TCP, UDP & Ports)]]**.