In the previous section, we learned that microservices can communicate by making HTTP requests to one another. This is known as **synchronous communication**, where one service waits for another service to respond before continuing.

While this works well in many situations, there are cases where waiting for an immediate response isn't necessary.

For example, when a vehicle's insurance is about to expire, the **Vehicle Service** doesn't need to wait for an email to be sent before continuing its work. It simply needs to notify another service that an expiry event has occurred.

This is where **asynchronous communication** becomes useful.

---

## What is Asynchronous Communication?

In **asynchronous communication**, one service sends a message or an event and continues its work immediately without waiting for another service to process it.

Instead of talking directly to another service, both services communicate through a **message broker** like **Kafka**.

```text
Vehicle Service
        │
Publishes Event
        ▼
      Kafka
        │
        ▼
Notification Service
```

This allows services to work independently while still collaborating with each other.

---

## Why Not Just Use HTTP?

Let's compare the two approaches.

### Synchronous Communication (HTTP)

```text
Vehicle Service
        │
        ▼
Notification Service
        │
        ▼
Email Sent
        │
        ▼
Vehicle Service Continues
```

The Vehicle Service has to wait until the Notification Service finishes its work.

---

### Asynchronous Communication (Kafka)

```text
Vehicle Service
        │
Publish Event
        ▼
      Kafka
        │
Vehicle Service Continues
        │
        ▼
Notification Service
        │
        ▼
Email Sent
```

Here, the Vehicle Service doesn't wait. It publishes an event and immediately continues processing other requests.

---

## What is Kafka?

**Apache Kafka** is a distributed event streaming platform that acts as a bridge between services.

Instead of one service sending requests directly to another, services exchange **events** through Kafka.

You can think of Kafka as a **message delivery system**.

- One service publishes a message.
    
- Kafka stores the message.
    
- Another service reads the message whenever it's ready.
    

Neither service needs to know whether the other is currently busy or even running.

---

## Producer and Consumer

In Kafka, there are two important roles.

### Producer

A **Producer** is the service that publishes events.

In our project:

```text
Vehicle Service
        │
Publishes Expiry Event
        ▼
      Kafka
```

---

### Consumer

A **Consumer** is the service that listens for events.

```text
Kafka
   │
   ▼
Notification Service
```

Whenever a new expiry event arrives, the Notification Service receives it and sends the email.

---

## Topics

Kafka organizes messages into **Topics**.

A topic is simply a named channel where related events are stored.

In AutoSentry, we used a topic similar to:

```text
vehicle-expiry-topic
```

The Vehicle Service publishes events to this topic, while the Notification Service listens to the same topic.

```text
Vehicle Service
        │
        ▼
vehicle-expiry-topic
        │
        ▼
Notification Service
```

---

## A Small Example

When the scheduler finds that a vehicle's insurance expires in two days, it publishes an event.

The code might look something like this:

```java
kafkaTemplate.send(
    "vehicle-expiry-topic",
    expiryEvent
);
```

On the other side, the Notification Service listens for new events.

```java
@KafkaListener(topics = "vehicle-expiry-topic")
public void handleExpiry(ExpiryEvent event) {
    // Send email
}
```

You don't need to understand every line of code right now. The important idea is that **one service publishes an event, while another service reacts to it**.

---

## Why Use Kafka?

Using Kafka provides several advantages:

- Services don't need to wait for each other.
    
- Producers and consumers remain independent.
    
- Events can still be processed even if a service is temporarily unavailable.
    
- Multiple services can react to the same event if needed.
    

This makes distributed systems more scalable and resilient.

---

## Complete Flow

```text
Daily Scheduler
        │
        ▼
Vehicle Service
        │
Insurance expires in 2 days
        │
        ▼
Publish Event
        │
        ▼
vehicle-expiry-topic (Kafka)
        │
        ▼
Notification Service
        │
        ▼
Send Email
```

Notice that the Vehicle Service never directly calls the Notification Service. Kafka acts as the communication bridge between them.

---

## HTTP vs Kafka

|HTTP Communication|Kafka Communication|
|---|---|
|Direct service-to-service communication|Communication through a message broker|
|Sender waits for a response|Sender continues immediately|
|Best when an immediate response is needed|Best for background processing and events|
|Tightly coupled communication|Loosely coupled communication|

---

## What's Next?

So far, we've explored how microservices communicate and collaborate to perform business operations. As the number of services grows, monitoring their health, performance, and logs becomes increasingly important.

In the next section, we'll learn how tools like **Spring Boot Actuator**, **Prometheus**, **Grafana**, and **Loki** help us monitor and observe a distributed microservices application.

➡️ **[[Monitoring & Observability]]**