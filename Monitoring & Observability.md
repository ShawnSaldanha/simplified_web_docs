Building a microservices application is only half the job. Once the application is deployed, we also need to ensure that it is running correctly.

Questions like these become important:

- Is every service running?
    
- How many requests is each service handling?
    
- Is any service becoming slow?
    
- Why did a particular request fail?
    
- What happened just before an error occurred?
    

Finding answers to these questions is the purpose of **monitoring** and **observability**.

During our AutoSentry project, we used **Spring Boot Actuator**, **Prometheus**, **Grafana**, and **Loki** to monitor the health, performance, and logs of our microservices.

---

## Monitoring vs Observability

Although these terms are often used together, they are slightly different.

### Monitoring

Monitoring focuses on collecting information about the current state of the application.

For example:

- Is the service running?
    
- How much CPU is being used?
    
- How many requests are received every minute?
    
- Is memory usage increasing?
    

Monitoring tells us **what is happening**.

---

### Observability

Observability helps us understand **why** something is happening.

If a service suddenly becomes slow, observability helps us investigate questions like:

- Which endpoint is slow?
    
- Did another service fail?
    
- What do the application logs say?
    
- When did the issue begin?
    

Observability helps developers diagnose and troubleshoot problems more effectively.

---

## Our Monitoring Stack

During the internship, we used the following tools together.

```text
Spring Boot Service
        │
        ├────────► Actuator
        │              │
        │              ▼
        │         Prometheus
        │              │
        │              ▼
        │           Grafana
        │
        └────────► Logs
                       │
                       ▼
                     Loki
                       │
                       ▼
                    Grafana
```

Each tool has a specific responsibility.

---

## Spring Boot Actuator

Every Spring Boot service exposes useful information about itself through **Actuator**.

Some examples include:

- Application health
    
- Memory usage
    
- Request statistics
    
- JVM information
    
- Application metrics
    

A typical Actuator endpoint looks like:

```text
/actuator/health
```

It may return something like:

```json
{
  "status": "UP"
}
```

This allows us to quickly verify whether a service is healthy.

---

## Prometheus

Prometheus is responsible for **collecting metrics**.

It periodically visits the Actuator endpoints of each microservice and stores the metrics in its own database.

```text
Actuator
     │
     ▼
Prometheus
     │
Stores Metrics
```

Examples of collected metrics include:

- Number of requests
    
- Response time
    
- Memory usage
    
- CPU usage
    
- JVM statistics
    

---

## Grafana

Prometheus stores the data, but reading raw numbers isn't very convenient.

Grafana connects to Prometheus and displays those metrics as dashboards, graphs, and charts.

Instead of seeing:

```text
CPU Usage = 37%
Memory = 512 MB
Requests = 180/min
```

we can view all of this information visually in a dashboard.

This makes it much easier to monitor the application's health over time.

---

## Loki

While Prometheus collects **metrics**, it does **not** store application logs.

That's where **Loki** comes in.

Each Spring Boot service writes logs using Logback. In our project, a Loki4j Logback Appender forwards these logs directly to Loki, where they are stored and later visualized in Grafana.

For example:

```text
Vehicle Service
-------------------------
Vehicle created successfully.

Insurance reminder sent.

Unable to connect to database.
```

These logs are stored by Loki and can later be searched whenever an issue occurs.

---

## Why Use Grafana with Loki?

Grafana isn't limited to metrics.

It can also display logs stored in Loki.

This means we can view both **performance metrics** and **application logs** from a single dashboard.

```text
Grafana Dashboard

CPU Usage
Memory Usage
Request Count

-------------------------

Application Logs

Vehicle created successfully

Insurance reminder sent

Database connection failed
```

Having both metrics and logs in one place makes debugging much easier.

---

## Complete Monitoring Flow

```text
                 Spring Boot Service
                  │             │
                  │             │
          Metrics │             │ Logs
                  ▼             ▼
             Actuator          Loki
                  │             │
                  ▼             │
             Prometheus         │
                  │             │
                  └──────┬──────┘
                         ▼
                     Grafana
```

Using this monitoring stack, we can easily track the health, performance, and behavior of our microservices in one place.

---

## Why Is This Important?

As the number of microservices increases, manually checking each service becomes difficult.

Monitoring tools allow us to quickly answer questions like:

- Is every service healthy?
    
- Which service is experiencing problems?
    
- Are requests becoming slower?
    
- What errors occurred recently?
    

This helps teams detect issues early and maintain reliable applications.

---

## What's Next?

So far, we've explored how microservices are designed, communicate, and are monitored in production.

The final piece is deployment. Instead of installing every dependency manually, we can package each service into a portable container and run the entire application consistently across different environments.

➡️ **[[Containerization with Docker]]**