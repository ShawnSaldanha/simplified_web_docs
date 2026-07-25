Imagine you want to send a parcel to your friend.

You can't simply write:

> **"To: Rahul"**

There could be thousands of people named Rahul. The delivery company needs a complete address to know exactly where the parcel should go.

Computers work the same way.

When one device wants to send data to another, it needs a unique address so the data knows where to go.

This unique address is called an **IP Address**.

---

## What is an IP Address?

An **IP (Internet Protocol) Address** is a unique address assigned to every device connected to a network.

It acts just like a home address.

Without it, devices wouldn't know where to send or receive data.

For example, when you visit:

```text
https://example.com
```

your browser eventually sends a request to a server using its IP address—not its domain name.

A simplified journey looks like this:

```text
Your Laptop
      │
      ▼
Needs Server's IP Address
      │
      ▼
Request Sent
      │
      ▼
Server
```

We'll learn later how the browser finds that IP address using **DNS**.

---

## Why Can't Computers Just Use Names?

Humans are good at remembering names.

Computers are better at working with numbers.

For example, which is easier for you to remember?

```text
google.com
```

or

```text
142.250.190.46
```

Most of us would choose the first one.

That's why we use domain names.

Behind the scenes, however, computers still communicate using IP addresses.

Think of it like this:

```text
You remember:
google.com

Computer understands:
142.250.xxx.xxx
```

The translation between the two is handled by **DNS**, which we'll explore in a later node.

---

# IPv4

The first widely adopted version of IP addressing is called **IPv4**.

An IPv4 address consists of **four numbers separated by dots**.

For example:

```text
192.168.1.25
```

Each number can range from **0 to 255**.

You'll often see addresses that look similar to these:

```text
10.0.0.15

172.16.1.5

192.168.0.100
```

These are perfectly valid IPv4 addresses.

For many years, IPv4 worked perfectly because there weren't many devices connected to the Internet.

But things changed.

---

## The Problem with IPv4

Today, almost everything connects to the Internet.

- Phones
    
- Laptops
    
- TVs
    
- Smartwatches
    
- Security cameras
    
- Smart speakers
    
- Cars
    
- Cloud servers
    

Every one of these devices needs an IP address.

Eventually, the world began running out of available IPv4 addresses.

Simply put,

there weren't enough unique addresses for every device on Earth.

A new solution was needed.

---

# IPv6

To solve this problem, **IPv6** was introduced.

Instead of providing billions of addresses, IPv6 provides an unimaginably large number of unique addresses.

An IPv6 address looks quite different.

```text
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

At first glance, it looks intimidating.

Fortunately, as developers, we rarely need to remember or type these addresses manually.

The important thing to know is simply this:

- **IPv4** was running out of addresses.
    
- **IPv6** was created to solve that problem.
    

Today, both IPv4 and IPv6 are used across the Internet.

---

# Public vs Private IP Addresses

Not every device on Earth needs a globally unique address.

Imagine a company with 2,000 computers.

Giving every computer a separate public Internet address would waste a huge number of IP addresses.

Instead, networks are divided into two types of addresses.

---

## Private IP Address

A **Private IP Address** is used **inside a local network**.

For example, inside your home Wi-Fi:

```text
Laptop
192.168.1.10

Phone
192.168.1.11

TV
192.168.1.12
```

These addresses are only meaningful inside your own network.

Another person's home can use the exact same addresses without causing any problems.

---

## Public IP Address

A **Public IP Address** is visible on the Internet.

This is the address assigned by your Internet Service Provider (ISP).

Interestingly,

although you may have ten devices connected to your home Wi-Fi,

they usually share **one public IP address**.

```text
               Internet
                    │
            Public IP
         49.xxx.xxx.xxx
                    │
             Home Router
          /      |      \
         /       |       \
 Laptop   Phone   Smart TV
192.168   192.168   192.168
```

You might now wonder:

> **How can multiple devices share one public IP address?**

The answer is **NAT (Network Address Translation)**, which we'll learn in **[[Routing, NAT & DNS]]**.

---

# What is CIDR?

As the Internet grew, engineers realized that allocating IP addresses in fixed-sized blocks wasn't very efficient.

Some organizations received far more addresses than they actually needed, while others didn't receive enough.

To solve this, a more flexible system called **CIDR (Classless Inter-Domain Routing)** was introduced.

Instead of fixed address groups, CIDR allows networks to be allocated based on their actual requirements.

You'll often see IP addresses written like this:

```text
192.168.1.0/24
```

The **"/24"** is called the **prefix length**.

It tells us:

> **How much of the address represents the network, and how much is available for devices inside that network.**

For now, you don't need to calculate these values manually.

Just remember that CIDR makes IP allocation much more flexible and efficient than older methods.

---

# Why Do We Need Subnetting?

Imagine a company with one giant network containing every employee.

```text
Company Network

HR

Engineering

Finance

Sales

Support

Marketing
```

As the company grows, this becomes difficult to manage.

- Too many devices.
    
- More unnecessary network traffic.
    
- Harder to organize departments.
    
- Reduced security.
    

A better solution is to split the large network into smaller ones.

This process is called **Subnetting**.

---

## What is Subnetting?

Subnetting simply means dividing one large network into multiple smaller networks.

For example:

```text
Company Network
        │
 ┌──────┼────────┐
 │      │        │
 ▼      ▼        ▼

HR   Engineering  Finance
Subnet  Subnet    Subnet
```

Each department now has its own smaller network.

This makes the overall network:

- Easier to manage.
    
- More organized.
    
- More secure.
    
- Better at handling network traffic.
    

Subnetting is commonly used in:

- Companies
    
- Universities
    
- Data centers
    
- Cloud platforms
    

As backend developers, we usually won't design subnet layouts ourselves, but we'll often encounter them when deploying applications to cloud providers like AWS, Azure, or Google Cloud.

---

## Classful vs Classless Addressing

Earlier, IP addresses were divided into fixed classes (Class A, Class B, Class C).

This approach is known as **Classful Addressing**.

The problem was that these fixed classes often wasted large numbers of IP addresses.

Modern networks instead use **Classless Addressing**, also known as **CIDR**, which allocates IP addresses based on actual requirements rather than fixed classes.

That's why almost every modern network today uses CIDR instead of the older class-based system.

---

## Key Takeaways

- Every device on a network needs a unique **IP Address**.
    
- Humans remember **domain names**, while computers communicate using **IP addresses**.
    
- **IPv4** is the original addressing system and is still widely used.
    
- **IPv6** was introduced because the world was running out of IPv4 addresses.
    
- **Private IP Addresses** are used inside local networks.
    
- **Public IP Addresses** are used on the Internet.
    
- **CIDR** allows IP addresses to be allocated more efficiently.
    
- **Subnetting** divides one large network into smaller, easier-to-manage networks.
    

---

## What's Next?

Now that every device has an IP address, another question naturally comes up:

> **If two devices are connected to the same local network, how do they actually find each other and exchange data?**

To answer that, we'll learn about **MAC Addresses**, **Ethernet Frames**, and **ARP**, which work together to deliver data within a local network.

Continue to **[[MAC Addresses, Ethernet & ARP]]**.