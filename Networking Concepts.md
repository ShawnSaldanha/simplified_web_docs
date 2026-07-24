Whenever we open a website, send a message, watch a YouTube video, or make an API request from our application, data has to travel from one device to another. But how does your laptop know where Google's servers are? How does a request travel across countries in just a few milliseconds? How does the server know where to send the response back?

The answer lies in **computer networking**.

Networking is what allows computers, servers, phones, and other devices to communicate with each other. It provides the rules, protocols, and infrastructure that make the modern internet possible.

As backend developers, understanding networking is extremely valuable. Every REST API we build, every database connection we make, and every request sent to our Spring Boot applications relies on networking concepts working behind the scenes.

---

## Why Should We Learn Networking?

When we first start building websites, it often feels like everything "just works."

We type a URL into the browser...

```text
https://example.com
```

...and within a second, the webpage appears.

But behind that simple action, many things happen almost instantly.

```text
Browser
    │
    ▼
DNS finds the server's IP address
    │
    ▼
Router forwards the request
    │
    ▼
Internet carries the data
    │
    ▼
Server receives the request
    │
    ▼
Spring Boot processes it
    │
    ▼
Database (if required)
    │
    ▼
Response travels back
    │
    ▼
Browser displays the webpage
```

Every box in this journey represents concepts that we'll explore throughout this section.

Once we understand these building blocks, many backend technologies—such as REST APIs, API Gateways, Docker networking, Kubernetes, cloud services, and microservices—become much easier to understand.

---

## What We'll Learn

We'll gradually follow the same journey that every request takes across the internet.

We'll begin by understanding how computers communicate and how different types of networks are organized.

Next, we'll learn how every device gets a unique address so that data knows exactly where to go.

We'll then explore how devices inside the same network communicate using MAC addresses and Ethernet before looking at how routers move packets between different networks across the internet.

After that, we'll understand why protocols like TCP and UDP exist, how reliable communication is achieved, and why every application uses specific port numbers.

Finally, we'll look at some of the most common internet protocols we use every day before understanding how all of these concepts fit together through the OSI and TCP/IP models.

By the end of this section, you should have a clear mental picture of how a single request travels from your browser all the way to a backend server and back again.

---

## Learning Path

This section is organized in the following order:

- **[[How Devices Communicate]]** – Learn what a network is, the different types of networks, and the role of networking devices like routers, switches, modems, firewalls, and network interface cards.
    
- **[[IP Addressing & Subnetting]]** – Understand why every device needs an IP address, the difference between IPv4 and IPv6, public and private IP addresses, CIDR notation, and why subnetting exists.
    
- **[[MAC Addresses, Ethernet & ARP]]** – Discover how devices communicate within the same local network using MAC addresses, Ethernet frames, and the Address Resolution Protocol (ARP).
    
- **[[Routing, NAT & DNS]]** – Follow how requests travel across different networks, how routers forward packets, why DNS translates domain names into IP addresses, and how NAT allows multiple devices to share a single public IP address.
    
- **[[Transport Layer (TCP, UDP & Ports)]]** – Learn how applications communicate reliably, why TCP and UDP exist, how ports identify different services, and how TCP establishes connections using the three-way handshake.
    
- **[[Common Internet Protocols]]** – Explore the protocols we use every day, including HTTP, HTTPS, FTP, SMTP, DHCP, DNS, and ICMP, and understand the problem each one solves.
    
- **[[OSI Model & TCP/IP Model]]** – Bring everything together by seeing how networking responsibilities are divided into layers and how the protocols we've learned fit into the real-world TCP/IP model.
    

---

## What's Next?

Now that we have a high-level understanding of what networking is and why it's important, let's begin with the fundamentals by understanding how computers are connected together and how they communicate within different types of networks.

Continue to **[[How Devices Communicate]]**.