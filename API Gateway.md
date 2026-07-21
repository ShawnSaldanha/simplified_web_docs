As we learned in the previous section, **Service Discovery** allows microservices to locate one another without relying on hardcoded network addresses. However, another important question remains:

> **How do external clients communicate with multiple microservices?**

Imagine an application consisting of several services:

- User Service
    
- Vehicle Service
    
- Notification Service
    

Without an API Gateway, the client would need to know the address of every individual service.

```text
                 Client
                 /  |  \
                /   |   \
               ▼    ▼    ▼
		    User  Vehicle Notification (Services)
	       
  n                           
```

This approach quickly becomes difficult to manage as the number of services increases.

---

## The Problem

Suppose the client wants to:

- Log in
    
- View registered vehicles
    
- Receive notifications
    

Without an API Gateway, the client must know:

- Which service provides each feature.
    
- The network address of every service.
    
- Which port each service is running on.
    

If a service changes its address or a new service is added, every client application may need to be updated.

This creates tight coupling between clients and backend services.

---

## What is an API Gateway?

An **API Gateway** acts as a **single entry point** for all incoming client requests.

Instead of communicating directly with individual microservices, clients send every request to the API Gateway.

The gateway then determines which microservice should handle the request and forwards it accordingly.

```text
                 Client
                    │
                    ▼
              API Gateway
          ┌────────┼────────┐
          ▼        ▼        ▼
    User Service  Vehicle Service  Notification Service
```

From the client's perspective, the entire backend appears as a single application.

---

## Request Routing

One of the primary responsibilities of an API Gateway is **routing**.

Each incoming request is examined and forwarded to the appropriate microservice.

For example:

|Client Request|Routed To|
|---|---|
|`/users/**`|User Service|
|`/vehicles/**`|Vehicle Service|
|`/notifications/**`|Notification Service|

This allows each service to focus only on its own business responsibilities.

---

## Working with Service Discovery

The API Gateway does not need to store fixed addresses for every service.

Instead, it works together with **Eureka Server**.

When a request arrives:

1. The gateway identifies which service should handle it.
    
2. It asks Eureka where that service is currently running.
    
3. Eureka returns the service's location.
    
4. The gateway forwards the request.
    

```text
                 Client
                    │
                    ▼
              API Gateway
                    │
      "Where is Vehicle Service?"
                    │
                    ▼
              Eureka Server
                    │
      "Vehicle Service is here."
                    │
                    ▼
             Vehicle Service
```

Because of this, services can move, restart, or scale without affecting clients.

---

## Centralizing Common Responsibilities

Another advantage of an API Gateway is that certain functionality only needs to be implemented once instead of inside every microservice.

Examples include:

- Authentication
    
- Authorization
    
- Request logging
    
- Rate limiting
    
- Cross-Origin Resource Sharing (CORS)
    

Instead of every service performing these tasks independently, the gateway can handle many of them before forwarding the request.

This keeps individual microservices focused on their own business logic.

---

## Why Use an API Gateway?

Without an API Gateway:

- Clients must know every service.
    
- Clients must know every service address.
    
- Backend changes can affect client applications.
    
- Common functionality is repeated across services.
    

With an API Gateway:

- Clients communicate with a single endpoint.
    
- Routing is handled automatically.
    
- Service locations remain hidden from clients.
    
- Common responsibilities can be centralized.
    
- Backend services remain independent.
    

---

## Complete Request Flow

A typical request in a microservices application looks like this:

```text
                 Client
                    │
                    ▼
              API Gateway
                    │
                    ▼
              Eureka Server
                    │
                    ▼
          Appropriate Microservice
                    │
                    ▼
                Database
                    │
                    ▼
             Response Returned
```

The client never communicates directly with the individual microservices. Instead, every request passes through the API Gateway, which routes it to the correct destination.

---

## What's Next?

So far, we've seen how clients communicate with the system through an **API Gateway** and how services discover one another using **Eureka**. The next step is understanding **how microservices communicate with each other** when a business operation requires information from another service.

➡️ **[[Inter-Service Communication]]**
