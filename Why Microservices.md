As software applications grow, they often become more complex, serving more users, handling larger amounts of data, and supporting new features. While a single application may work well in the beginning, continuously adding new functionality can eventually make it difficult to maintain, scale, and deploy. This challenge led to the adoption of **microservices architecture**, where an application is broken down into multiple smaller, independent services, each responsible for a specific business capability.

Before understanding what microservices are, it's helpful to first understand the architecture they were designed to replace.

---

## Monolithic Architecture

A **monolithic application** is one where all features of the application are built, deployed, and run as a single unit. Components such as user management, authentication, payments, inventory, and notifications all exist within the same application and share the same codebase.

A typical monolithic application might look like this:

```text
                Monolithic Application
    ┌─────────────────────────────────────────┐
    │                                         │
    │  Authentication                         │
    │  User Management                        │
    │  Vehicle Management                     │
    │  Notification Service                   │
    │  Payment Processing                     │
    │                                         │
    └─────────────────────────────────────────┘
                    │
                    ▼
                 Database
```

For small applications, this approach is often simple to build and manage. However, as the application grows, maintaining a single large codebase becomes increasingly difficult.

---

## Challenges of a Monolithic Architecture

As a monolithic application grows, several challenges begin to appear.

### Difficult to Scale

Suppose only the **Notification** feature receives heavy traffic.

With a monolithic application, we cannot scale just that feature. Instead, the **entire application** must be deployed on additional servers, even if the rest of the application is handling very little traffic.

---

### Slower Development

Since all features exist within the same project, multiple developers often work on the same codebase simultaneously. As the project grows, coordinating changes becomes more difficult, increasing the likelihood of merge conflicts and making development slower.

---

### Full Application Deployment

Even a small change requires redeploying the entire application.

For example, fixing a typo in the notification module still requires building and deploying the whole application instead of only the affected component.

---

### Reduced Fault Isolation

If one part of the application consumes excessive memory or crashes unexpectedly, it can affect the stability of the entire application because all features run within the same process.

---

## Microservices Architecture

A **microservices architecture** addresses many of these challenges by dividing the application into multiple independent services. Each service is responsible for a specific business capability, has its own codebase, and can be developed, deployed, and scaled independently.

Instead of one large application, we now have several smaller services working together.

```text
                    Client
                       │
                       ▼
                 API Gateway
                       │
       ┌───────────────┼───────────────┐
       ▼               ▼               ▼
 User Service    Vehicle Service   Notification Service
       │               │               │
       ▼               ▼               ▼
   Database        Database        Database
```

Although these services are independent, they communicate with one another over the network to provide a seamless experience to the user.

---

## Advantages of Microservices

Compared to a monolithic architecture, microservices provide several benefits:

|Monolithic Architecture|Microservices Architecture|
|---|---|
|Single large application|Multiple smaller services|
|Entire application is deployed together|Each service can be deployed independently|
|Scaling affects the whole application|Individual services can be scaled independently|
|One failure can impact the entire application|Failures are better isolated to individual services|
|Single shared codebase|Independent services focused on specific responsibilities|

---

## Are Microservices Always Better?

Not necessarily.

Microservices solve many problems, but they also introduce new challenges. Since services run independently, they must communicate over a network, discover each other's locations, exchange data reliably, and be monitored individually. These additional requirements increase the complexity of the overall system.

For small applications, a monolithic architecture is often simpler and easier to maintain. Microservices become more beneficial as applications grow in size, complexity, and the number of developers working on them.

---

## What's Next?

Now that we understand **why** applications are divided into multiple services, the next step is to understand **what a single microservice actually looks like internally**. We'll explore the common structure of a Spring Boot microservice and the responsibilities of components such as controllers, services, repositories, entities, and DTOs.

➡️ **[[Anatomy of a Microservice]]**
