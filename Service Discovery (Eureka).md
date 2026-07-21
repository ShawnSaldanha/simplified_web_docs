As we learned in the previous section, a microservices application consists of multiple independent services. However, these services often need to communicate with one another to complete a business operation.

For example, a **Notification Service** may need information from the **User Service**, or a **Vehicle Service** may need to send an event that another service responds to.

This raises an important question:

> **How does one microservice know where another microservice is running?**

---

## The Problem with Hardcoded URLs

Imagine we have two services:

- User Service
    
- Vehicle Service
    

If the Vehicle Service needs to retrieve user information, we might initially configure it like this:

```text
Vehicle Service
        │
        ▼
http://localhost:8081/users
```

This works during development, but it quickly becomes a problem as the application grows.

Suppose the User Service is moved to another server or starts running on a different port.

```text
Old Address:
http://localhost:8081

New Address:
http://localhost:9090
```

Now every service that communicates with the User Service must be updated with the new address and redeployed.

In a large system with dozens of microservices, managing these hardcoded addresses becomes difficult and error-prone.

---

## What is Service Discovery?

**Service Discovery** is a mechanism that allows microservices to automatically find and communicate with one another without relying on hardcoded network addresses.

Instead of remembering where every service is running, each service registers itself with a central registry when it starts.

Other services can then ask the registry for the current location of the service they need.

---

## Eureka Server

In the Spring ecosystem, this registry is commonly provided by **Eureka Server**.

When a microservice starts, it registers itself with Eureka.

```text
          Eureka Server
          ┌──────────────┐
          │ User Service │
          │ Vehicle Svc  │
          │ Notify Svc   │
          └──────────────┘
```

The Eureka Server maintains a list of all active services and their current network locations.

---

## How Service Discovery Works

The communication flow now becomes much simpler.

```text
             Vehicle Service
                    │
     "Where is User Service?"
                    │
                    ▼
             Eureka Server
                    │
      "User Service is here"
                    │
                    ▼
             User Service
```

Instead of storing service addresses manually, the Vehicle Service simply asks Eureka where the User Service is currently running.

---

## Dynamic Registration

One of the biggest advantages of service discovery is that services register themselves automatically.

Whenever a service starts:

1. It registers itself with Eureka.
    
2. Eureka stores its network address.
    
3. Other services can immediately discover it.
    

If the service stops or becomes unavailable, Eureka removes it from the registry so other services no longer attempt to communicate with it.

This allows the system to adapt automatically as services start, stop, or move to different machines.

---

## Why is Service Discovery Important?

Without service discovery:

- Every service must know the address of every other service.
    
- Configuration becomes difficult to manage.
    
- Moving services requires updating multiple applications.
    
- Scaling services becomes more complicated.
    

With service discovery:

- Services locate each other automatically.
    
- Network addresses remain hidden from application code.
    
- Services can be moved without affecting other services.
    
- Scaling and deployment become much simpler.
    

---

## Where Does the API Gateway Fit?

In many microservices applications, external clients do **not** communicate directly with individual services.

Instead, requests first arrive at an **API Gateway**, which uses service discovery to determine where each request should be routed.

A simplified architecture looks like this:

```text
                 Client
                    │
                    ▼
              API Gateway
                    │
                    ▼
             Eureka Server
                    │
      ┌─────────────┼─────────────┐
      ▼             ▼             ▼
 User Service  Vehicle Service  Notification Service
```

This allows both the API Gateway and the individual microservices to discover services dynamically without relying on fixed URLs.

---

## Complete Flow

The overall service discovery process can be summarized as follows:

```text
1. A microservice starts.

        │
        ▼

2. It registers itself with Eureka Server.

        │
        ▼

3. Another service needs to communicate with it.

        │
        ▼

4. It asks Eureka for the service's location.

        │
        ▼

5. Eureka returns the current network address.

        │
        ▼

6. The services communicate directly.
```

---

## What's Next?

Now that we understand **how microservices discover one another**, the next step is to see **how external client requests are routed into the system** through a single entry point known as an **API Gateway**.

➡️ **[[API Gateway]]**
