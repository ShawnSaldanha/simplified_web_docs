In a microservices architecture, each service is responsible for a specific part of the application. However, a single user request often requires information from multiple services.

For example, suppose a user wants to view all their registered vehicles. The **Vehicle Service** can retrieve the vehicle details, but it may also need the user's information from the **User Service** before returning the final response.

This means that **microservices don't work in isolation—they frequently need to communicate with one another.**

---

## Why Do Services Need to Communicate?

Let's take our project where users can register their vehicles as an example.

Imagine a request like this:

```text
Show me all vehicles registered by Jon.
```

The request reaches the **Vehicle Service**.

The Vehicle Service knows everything about vehicles, but it doesn't store information about users.

Instead of storing duplicate user data, it simply asks the **User Service** for the required information.

```text
                Vehicle Service
                       │
     "Give me user details for User ID 15"
                       │
                       ▼
                User Service
                       │
                       ▼
              Returns User Details
```

Each service focuses only on its own responsibility, keeping the system clean and easier to maintain.

---

## Synchronous Communication

One of the most common ways for microservices to communicate is by making **HTTP requests** to one another.

This is called **synchronous communication** because one service waits for the other service to respond before continuing.

```text
Vehicle Service
        │
        ▼
HTTP Request
        │
        ▼
User Service
        │
        ▼
HTTP Response
        │
        ▼
Vehicle Service
```

It's very similar to how a frontend sends requests to a backend API—except now, the client is another microservice.

---

## A Simple Example

Suppose the Vehicle Service needs user information.

It might send a request like this:

```http
GET /users/15
```

The User Service responds with:

```json
{
  "id": 15,
  "name": "Jon Jones",
  "email": "Jon@example.com"
}
```

The Vehicle Service can now combine this information with its own data before sending the final response to the client.

---

## How Does It Know Where the User Service Is?

Earlier, we learned about **Service Discovery (Eureka)**.

Instead of using a hardcoded address like:

```text
http://localhost:8081
```

the Vehicle Service simply asks Eureka where the User Service is currently running.

This allows services to communicate even if their addresses change.

---

## REST Communication in Spring Boot

In Spring Boot, one microservice can call another using an HTTP client.

The actual implementation may vary, but conceptually it looks something like this:

```java
UserDto user = userServiceClient.getUserById(userId);
```

The important idea isn't the code itself—it's that one service is making an API call to another service.

---

## Is This Always the Best Approach?

Not always.

Synchronous communication is simple and works well when one service immediately needs data from another.

However, because one service has to wait for the other, slow or unavailable services can affect the overall response time.

For situations where an immediate response isn't required—such as sending emails or processing background tasks—we often use **asynchronous communication**, where services exchange events instead of waiting for direct responses.

We'll explore that in the next section.

---

## Complete Flow

```text
             Client
                │
                ▼
         Vehicle Service
                │
                │ HTTP Request
                ▼
          User Service
                │
                ▼
          User Database
                │
                ▼
          User Service
                │
                ▼
         Vehicle Service
                │
                ▼
             Client
```

Although multiple services work together behind the scenes, the client receives a single response without needing to know how the communication happened.

---

## What's Next?

So far, we've looked at **synchronous communication**, where one service waits for another to respond.

In many real-world systems, however, services don't always need an immediate response. Instead, they communicate by publishing and consuming events.

We'll explore this approach in the next topic:

➡️ **[[Asynchronous Communication (Kafka)]]**
