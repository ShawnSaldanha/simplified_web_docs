A **microservice** is an independent application responsible for a single business capability. Although multiple microservices work together to form a complete system, each service has its own codebase, business logic, and often its own database.

While different technologies may organize their projects differently, most backend microservices follow a layered architecture that separates responsibilities. This separation makes the code easier to understand, maintain, and test.

Let's see how a typical Spring Boot microservice is organized.

---

## Typical Project Structure

A simplified microservice project might look like this:

```text
vehicle-service/
│
├── controller/
├── service/
├── repository/
├── entity/
├── dto/
├── config/
├── exception/
└── VehicleServiceApplication.java
```

Each folder has a specific responsibility, allowing different parts of the application to remain independent and organized.

---

## How a Request Flows

Whenever a client sends a request, it passes through several layers before reaching the database.

```text
        Client
          │
          ▼
    Controller
          │
          ▼
      Service
          │
          ▼
    Repository
          │
          ▼
      Database
```

Once the database responds, the data travels back through the same layers until the response is returned to the client.

---

## Controller

The **Controller** is the entry point of the microservice.

It receives incoming HTTP requests, extracts any required information such as path variables or request bodies, and forwards the request to the appropriate service.

The controller should remain lightweight. Its primary responsibility is handling HTTP communication rather than implementing business logic.

Examples of responsibilities include:

- Receiving client requests
    
- Validating basic request data
    
- Calling the appropriate service
    
- Returning HTTP responses
    

---

## Service

The **Service** layer contains the application's business logic.

This is where the application decides **what should happen** after receiving a request. Services may perform calculations, validate business rules, communicate with other microservices, publish events, or retrieve data from the database.

Unlike controllers, services focus entirely on business operations rather than HTTP communication.

---

## Repository

The **Repository** layer is responsible for interacting with the database.

Instead of writing SQL queries throughout the application, repositories provide a clean way to save, update, delete, and retrieve data.

This separation allows the rest of the application to remain independent of database implementation details.

---

## Entity

An **Entity** represents how data is stored inside the database.

Each entity usually maps to a database table, with its fields representing table columns.

For example:

```text
Vehicle
------------------------
id
vehicleNumber
ownerName
insuranceExpiry
pollutionExpiry
```

The repository uses entities to read and write data to the database.

---

## DTO (Data Transfer Object)

A **DTO** is used to transfer data between different parts of the application or between the server and the client.

Instead of exposing the entire entity, the application can send only the information required by the client.

For example, the database may store many fields about a vehicle, but an API endpoint may only need to return the vehicle number and owner name. A DTO helps achieve this while keeping internal data protected.

---

## Configuration

The **Config** package contains application configuration.

This is where components such as security settings, API Gateway configuration, Kafka configuration, CORS settings, or other application-wide beans are typically defined.

Keeping configuration separate from business logic improves readability and maintainability.

---

## Exception Handling

Unexpected situations such as invalid input, missing records, or server errors should be handled gracefully.

Rather than allowing errors to propagate throughout the application, a dedicated exception handler converts them into meaningful HTTP responses that clients can understand.

This keeps error handling consistent across the entire microservice.

---

## Why Separate Everything?

At first, having many folders may seem unnecessary.

However, separating responsibilities makes applications much easier to develop and maintain.

For example:

- Controllers only handle HTTP requests.
    
- Services contain business logic.
    
- Repositories interact with the database.
    
- Entities represent stored data.
    
- DTOs transfer data safely.
    
- Configuration manages application setup.
    
- Exception handlers provide consistent error responses.
    

Because each layer has a single responsibility, the code becomes easier to understand, modify, test, and extend as the application grows.

---

## Complete Flow

A typical request inside a microservice follows this path:

```text
                 Client
                    │
                    ▼
              Controller
                    │
                    ▼
                Service
                    │
        ┌───────────┴───────────┐
        ▼                       ▼
 Repository           Other Microservices
        │                       │
        ▼                       ▼
    Database                REST / Kafka
                    │
                    ▼
              Response to Client
```

Although a microservice is independent, it often communicates with databases and other services to complete a business operation.

---

## What's Next?

Now that we understand how an individual microservice is structured internally, the next step is to understand **how multiple microservices find and communicate with one another** without relying on hardcoded network addresses.

➡️ **[[Service Discovery (Eureka)]]**
