Every day, we send messages on WhatsApp, watch YouTube videos, browse websites, and use cloud applications without giving much thought to what happens behind the scenes.

Although it feels instant, every one of these actions involves one device communicating with another.

Your phone talks to a server.

Your laptop talks to a printer.

Your backend application talks to a database.

Your microservices communicate with each other.

This communication between devices is what we call **networking**.

Simply put, a **network** is a group of devices connected together so they can exchange information and share resources.

---

## Why Do We Need Networks?

Imagine if every computer worked completely alone.

- You couldn't browse the internet.
    
- You couldn't send emails.
    
- You couldn't watch Netflix.
    
- You couldn't share files with friends.
    
- Cloud storage like Google Drive wouldn't exist.
    

Every computer would only know about itself.

Networking solves this problem by allowing devices to communicate with one another.

```text
Computer A
     │
     │  Data
     ▼
Computer B
```

Now imagine connecting millions—or even billions—of devices together.

That's exactly what the Internet is.

---

## Different Types of Networks

Not every network is the size of the Internet.

Depending on how large the area is, networks are divided into different categories.

---

### PAN (Personal Area Network)

A **PAN** connects devices that are very close to a single person.

Some common examples are:

- Phone ↔ Smartwatch
    
- Phone ↔ Wireless Earbuds
    
- Laptop ↔ Bluetooth Mouse
    

These usually communicate using Bluetooth or USB.

Think of a PAN as **your personal network**.

---

### LAN (Local Area Network)

A **LAN** connects devices within a small area like:

- A home
    
- An office
    
- A college lab
    
- A company building
    

For example, your home Wi-Fi creates a LAN.

```text
             WiFi Router
           /      |      \
          /       |       \
      Laptop   Mobile   Smart TV
```

All these devices can communicate with one another because they're part of the same local network.

During our internship, whenever we connected our laptops to the office Wi-Fi, we were joining the company's LAN.

---

### MAN (Metropolitan Area Network)

A **MAN** connects multiple LANs across a city or a large campus.

For example:

- A university connecting all its departments.
    
- A company connecting multiple office buildings in the same city.
    

We don't usually build MANs ourselves as developers, but it's useful to know they exist.

---

### WAN (Wide Area Network)

A **WAN** connects networks over very large distances.

Instead of connecting devices inside one building, it connects entire cities, countries, or even continents.

The biggest example of a WAN is...

**The Internet.**

When your laptop in India accesses a server in the United States, your request travels across a massive Wide Area Network.

---

### VPN (Virtual Private Network)

Sometimes we want to securely access a private network even when we're somewhere else.

That's where a **VPN** comes in.

A VPN creates an encrypted connection between your device and another network over the Internet.

For example, many companies allow employees to work from home by first connecting to the company's VPN.

```text
Your Laptop
      │
Encrypted Connection
      │
      ▼
Company Network
```

To your laptop, it almost feels as if you're sitting inside the office.

---

## How Are These Devices Connected?

Simply having multiple computers isn't enough.

There also needs to be hardware that helps them communicate.

Let's look at the most common networking devices.

---

## Router

A **router** connects different networks together.

Think of it as a traffic police officer.

Whenever data arrives, the router decides:

> "Which road should this packet take to reach its destination?"

For example:

```text
Your Laptop
      │
      ▼
Router
      │
      ▼
Internet
```

Without routers, data wouldn't know where to go.

Every time you visit a website, your request passes through several routers before reaching the destination server.

We'll learn much more about routing later in **[[Routing, NAT & DNS]]**.

---

## Switch

A **switch** connects multiple devices within the **same local network**.

Unlike a router, it doesn't send data across the Internet.

Instead, it helps devices inside the same LAN communicate efficiently.

For example, in an office:

```text
          Switch
       /    |    \
      /     |     \
 PC 1    PC 2   Printer
```

If PC 1 wants to send data to the printer, the switch forwards it directly to the printer instead of broadcasting it to every device.

You can think of a switch as an efficient receptionist inside an office who knows exactly where everyone sits.

---

## Modem

Your home router doesn't magically connect to the Internet.

It first needs to communicate with your **Internet Service Provider (ISP)**.

That's the job of a **modem**.

A modem acts as a bridge between your home network and your ISP.

A simplified view looks like this:

```text
Laptop
   │
WiFi Router
   │
Modem
   │
ISP
   │
Internet
```

Many modern home routers actually have the modem built into the same device, which is why we often don't notice it separately.

---

## Firewall

Not every request coming from the Internet should be trusted.

A **firewall** acts like a security guard standing at the entrance of a network.

It checks incoming and outgoing traffic and decides:

- Allow this.
    
- Block this.
    

Firewalls help protect systems from unauthorized access and malicious traffic.

Many cloud providers, operating systems, and even home routers include built-in firewalls.

---

## Network Interface Card (NIC)

Every device needs a way to physically connect to a network.

That's the job of a **Network Interface Card**, usually called a **NIC**.

Whether you're using:

- Wi-Fi
    
- Ethernet cable
    

your device uses its NIC to send and receive network data.

Without a NIC, your computer wouldn't be able to communicate with any network at all.

---

## Putting Everything Together

Let's see what happens when you open a website at home.

```text
Your Laptop
      │
      ▼
Network Interface Card (NIC)
      │
      ▼
WiFi Router
      │
      ▼
Modem
      │
      ▼
Internet Service Provider
      │
      ▼
Internet
      │
      ▼
Website Server
```

Although this entire journey happens in just a fraction of a second, many networking devices work together to ensure your request reaches the correct destination.

As backend developers, we don't usually configure routers or switches ourselves, but understanding their role helps us understand **how our applications communicate with users across the Internet**.

---

## Key Takeaways

- A **network** allows multiple devices to communicate and share resources.
    
- Networks come in different sizes, such as **PAN, LAN, MAN, WAN, and VPN**.
    
- A **router** connects different networks together.
    
- A **switch** connects devices within the same local network.
    
- A **modem** connects your local network to your Internet Service Provider.
    
- A **firewall** protects a network by filtering traffic.
    
- A **NIC** allows a device to connect to a network.
    

---

## What's Next?

Now that we know how devices are connected, the next question is:

> **How does every device get its own unique identity so that data knows exactly where to go?**

To answer that, we'll learn about **IP addresses**, the difference between **IPv4 and IPv6**, and why concepts like **CIDR** and **subnetting** exist.

Continue to **[[IP Addressing & Subnetting]]**.