As our application grew from a single Spring Boot project into multiple microservices, running everything manually became increasingly difficult.

For our AutoSentry project, we had several components running simultaneously:

- PostgreSQL
    
- Kafka
    
- MailHog
    
- Eureka Server
    
- API Gateway
    
- User Service
    
- Vehicle Service
    
- Notification Service
    
- Prometheus
    
- Grafana
    
- Loki
    

Starting each service individually, ensuring they all had the correct configuration, and making sure they could communicate with one another quickly became tedious.

This is where **Docker** made our lives much easier.

---

## What is Docker?

Docker is a platform that packages an application along with everything it needs to run into a **container**.

Instead of saying,

> "Install Java 21, PostgreSQL, Kafka, and then run these commands..."

we can simply say,

> "Run this Docker container."

Everything required by the application is already packaged inside it.

---

## What is a Container?

A container is an isolated environment where an application runs.

Think of it like giving every service its own small computer.

```text
+------------------------+
| Vehicle Service        |
| Java                   |
| Dependencies           |
| Configuration          |
+------------------------+

+------------------------+
| User Service           |
| Java                   |
| Dependencies           |
| Configuration          |
+------------------------+
```

Although all containers share the same operating system, each one behaves independently.

---

## Dockerfile

Before Docker can create a container, it needs instructions.

These instructions are written in a **Dockerfile**.

A Dockerfile answers questions like:

- Which base image should be used?
    
- Where is the application JAR located?
    
- Which port does the application use?
    
- What command starts the application?
    

A simplified Dockerfile might look like:

```dockerfile
FROM eclipse-temurin:21-jdk

COPY target/app.jar app.jar

EXPOSE 8081

ENTRYPOINT ["java", "-jar", "app.jar"]
```

When Docker reads this file, it builds an **image**.

---

## Image vs Container

This is one of the most confusing concepts for beginners.

An **Image** is a blueprint.

A **Container** is a running instance created from that blueprint.

```text
Dockerfile
      │
      ▼
 Docker Image
      │
 docker run
      ▼
 Docker Container
```

Just like a Java class can create multiple objects, one Docker image can create multiple containers.

---

## Docker Compose

Imagine starting every container manually.

```text
docker run postgres
docker run kafka
docker run eureka
docker run user-service
docker run vehicle-service
...
```

That would be inconvenient.

Instead, Docker Compose allows us to describe the entire application in a single `docker-compose.yml` file.

In our project, Docker Compose started:

- PostgreSQL
    
- Kafka
    
- MailHog
    
- Eureka
    
- API Gateway
    
- All microservices
    
- Prometheus
    
- Grafana
    
- Loki
    

with a single command:

```bash
docker compose up
```

---

## How Do Containers Communicate?

Every container has its own isolated network.

If no special configuration is provided, containers cannot simply communicate with each other.

Docker Compose solves this by creating a shared network.

In our project:

```yaml
networks:
  autosentry-net:
```

Every service joined this network.

```text
          autosentry-net

   User Service
         │
Vehicle Service
         │
Notification Service
         │
    PostgreSQL
         │
       Kafka
```

Because all containers are connected to the same network, they can communicate using their **service names**.

For example:

Instead of

```text
localhost:5432
```

the Vehicle Service connects to

```text
autosentry-db:5432
```

Similarly,

```text
autosentry-kafka:9092
```

instead of

```text
localhost:9092
```

Docker automatically resolves these service names to the correct container.

---

## Why Doesn't localhost Work?

This is a common point of confusion.

Inside a container,

```text
localhost
```

refers to **that container itself**, not your computer.

For example,

```text
Vehicle Service Container

localhost
      │
      ▼
Vehicle Service
```

It **does not** point to PostgreSQL or Kafka.

To reach another container, we use its service name.

```text
Vehicle Service
       │
       ▼
autosentry-db
```

Docker's internal network handles the rest.

---

## Container Ports vs Host Ports

Each container has its own ports.

For example, our Vehicle Service listens on:

```text
8082
```

inside its container.

However, our computer cannot access that port directly.

We expose it using Docker Compose.

```yaml
ports:
  - "8082:8082"
```

The format is:

```text
HOST_PORT : CONTAINER_PORT
```

```text
Your Computer
localhost:8082
       │
       ▼
Vehicle Service Container
       │
Port 8082
```

This mapping allows applications outside Docker, such as your browser or Postman, to communicate with services running inside containers.

---

## How Everything Works Together

When we ran:

```bash
docker compose up
```

Docker performed the following steps:

1. Built images from each Dockerfile.
    
2. Created containers from those images.
    
3. Connected every container to `autosentry-net`.
    
4. Started PostgreSQL, Kafka, Eureka, and the other infrastructure services.
    
5. Started each Spring Boot microservice.
    
6. Exposed the required ports to our local machine.
    

The result was a fully working distributed system that could be started with a single command.

---

## Complete Deployment Flow

```text
              Docker Compose
                     │
      ┌──────────────┼──────────────┐
      ▼              ▼              ▼
 Dockerfile     Dockerfile     Dockerfile
(User)         (Vehicle)      (Gateway)
      │              │              │
      ▼              ▼              ▼
 Docker Image   Docker Image   Docker Image
      │              │              │
      ▼              ▼              ▼
 Docker Container Docker Container Docker Container
      │              │              │
      └──────────────┼──────────────┘
                     │
             autosentry-net
                     │
     PostgreSQL • Kafka • MailHog
                     │
              Prometheus • Loki
                     │
                  Grafana
```

---

## Why Use Docker?

Docker offers several benefits:

- Applications run consistently across different machines.
    
- Every developer works with the same environment.
    
- Dependencies don't have to be installed manually.
    
- Microservices can communicate easily using Docker networks.
    
- The entire application can be started or stopped with a single command.
    

---

## What's Next?

Congratulations! 🎉

We've now explored the core concepts behind building and operating a distributed microservices application from understanding why microservices exist to deploying them with Docker.

