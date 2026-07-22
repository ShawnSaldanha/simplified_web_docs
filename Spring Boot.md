In the previous section, we learned how the **Spring Framework** simplifies Java development by managing object creation, handling dependencies, and providing a structured way to build applications.

However, developers still faced another problem.

Although Spring made development much easier, creating a Spring application still required a considerable amount of manual configuration before writing any actual business logic.

This is where **Spring Boot** comes in.

Spring Boot builds on top of the Spring Framework and removes much of the repetitive configuration, allowing developers to focus on building applications instead of setting them up.

---

# Why Was Spring Boot Created?

Imagine you're asked to build a simple REST API using the traditional Spring Framework.

You might expect to immediately start writing Controllers and Services.

Instead, the first few hours—or even days—could be spent configuring the project.

Some of the tasks included:

- Adding dozens of dependencies manually.
    
- Configuring XML files (especially in older Spring versions).
    
- Setting up the Dispatcher Servlet.
    
- Configuring database connections.
    
- Configuring logging.
    
- Packaging the application correctly.
    
- Deploying it to an external web server.
    

Before writing business logic, developers had to spend significant time configuring infrastructure.

---

# The Traditional Spring Workflow

A typical Spring application looked something like this:

```text
Write Spring Code
        │
        ▼
Compile Project
        │
        ▼
Package as WAR File
        │
        ▼
Install Apache Tomcat
        │
        ▼
Copy WAR into Tomcat
        │
        ▼
Start Tomcat Server
        │
        ▼
Application Runs
```

Notice how many manual steps were involved before the application could even start.

---

# What is a WAR File?

A **WAR (Web Application Archive)** is simply a packaged version of a Java web application.

You can think of it as a ZIP file containing:

- Compiled Java classes
    
- HTML pages
    
- Configuration files
    
- Static resources
    
- Libraries
    

However, a WAR file cannot run by itself.

It needs a web server like **Apache Tomcat** to execute it.

This meant every developer first had to install Tomcat separately before running the application.

---

# The Problem with External Servers

Suppose every developer on your team installs Tomcat manually.

Immediately, new problems appear.

```text
Developer A
Tomcat 8

Developer B
Tomcat 9

Developer C
Tomcat 10
```

Different versions...

Different configurations...

Different environments...

The same application might work perfectly on one machine but fail on another.

Deploying applications also became more complicated because the WAR file always had to be copied into the server manually.

There had to be a better solution.

---

# Spring Boot's Solution

Spring Boot completely changed how Java applications are deployed.

Instead of deploying our application **to Tomcat**,

Spring Boot places **Tomcat inside the application itself**.

This is called an **Embedded Server**.

Now the workflow becomes much simpler.

```text
Write Spring Boot Code
          │
          ▼
Run main()
          │
          ▼
Embedded Tomcat Starts
          │
          ▼
Application Runs
```

No separate Tomcat installation.

No WAR deployment.

Everything is packaged together.

---

# Embedded Tomcat

Whenever we create a Spring Boot web application, Spring Boot automatically includes an embedded web server.

Usually this is:

- Apache Tomcat (default)
    
- Jetty
    
- Undertow
    

When we run:

```java
public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
}
```

Spring Boot performs several tasks automatically.

```text
Start Application
        │
        ▼
Create Spring Container
        │
        ▼
Create all Beans
        │
        ▼
Start Embedded Tomcat
        │
        ▼
Begin listening for HTTP requests
```

That's why we simply click **Run** inside our IDE and immediately have a working web server.

---

# Auto Configuration

One of Spring Boot's biggest features is **Auto Configuration**.

Instead of asking us to configure everything manually,

Spring Boot examines the project's dependencies and automatically configures many components.

For example,

if Spring Boot detects

```xml
spring-boot-starter-web
```

it automatically configures:

- Embedded Tomcat
    
- Spring MVC
    
- Dispatcher Servlet
    
- JSON conversion
    
- HTTP request handling
    

without requiring additional configuration.

---

# Starter Dependencies

Imagine adding every required library manually.

A web application might need:

- Spring MVC
    
- Jackson
    
- Tomcat
    
- Validation
    
- Logging
    
- Servlet API
    

Instead of adding every dependency individually,

Spring Boot groups related dependencies into **Starter Dependencies**.

For example,

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

This single dependency downloads everything required for building REST APIs.

Similarly,

```text
spring-boot-starter-data-jpa
```

contains everything required for database development.

Some commonly used starters are:

- spring-boot-starter-web
    
- spring-boot-starter-security
    
- spring-boot-starter-data-jpa
    
- spring-boot-starter-validation
    
- spring-boot-starter-test
    

---

# The @SpringBootApplication Annotation

Every Spring Boot project starts with a class similar to this.

```java
@SpringBootApplication
public class AutoSentryApplication {

    public static void main(String[] args) {
        SpringApplication.run(AutoSentryApplication.class, args);
    }

}
```

Although this looks like a single annotation, it actually combines multiple Spring annotations together.

It tells Spring Boot:

- Start the application.
    
- Create the Spring Container.
    
- Scan for Spring Beans.
    
- Apply Auto Configuration.
    

This becomes the entry point of the application.

---

# Configuration Files

Almost every application has configurable values.

For example:

- Database URL
    
- Database Username
    
- Server Port
    
- JWT Secret
    
- Kafka Address
    

Instead of hardcoding these values inside Java classes,

Spring Boot stores them inside:

```text
application.properties
```

or

```text
application.yml
```

Example:

```yaml
server:
  port: 8082

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/vehicle_db
```

This makes changing application settings much easier.

---

# Building REST APIs

One of Spring Boot's primary purposes is building REST APIs.

A typical request flows like this.

```text
Client
    │
HTTP Request
    │
    ▼
Controller
    │
Business Logic
    ▼
Service
    │
Database Operations
    ▼
Repository
    │
    ▼
Database
```

Each layer has a specific responsibility.

- Controller receives requests.
    
- Service contains business logic.
    
- Repository communicates with the database.
    

Keeping responsibilities separate makes applications much easier to maintain.

---

# Spring Boot in Our AutoSentry Project

In our AutoSentry project, every service is an independent Spring Boot application.

For example,

```text
User Service

Vehicle Service

Notification Service

API Gateway

Eureka Server
```

Each service has:

- Its own Spring Boot project.
    
- Its own embedded Tomcat server.
    
- Its own configuration.
    
- Its own business logic.
    

These services communicate with one another to form our complete microservices architecture.

---

# Why is Spring Boot So Popular?

Spring Boot offers several advantages:

- Minimal configuration.
    
- Embedded web servers.
    
- Auto Configuration.
    
- Starter Dependencies.
    
- Faster development.
    
- Production-ready features.
    
- Easy integration with databases, security, messaging systems, and cloud technologies.
    

Instead of spending time configuring infrastructure, developers can immediately begin building application features.

---

# Spring Framework vs Spring Boot

|Spring Framework|Spring Boot|
|---|---|
|Provides the core framework for Java applications.|Builds on top of Spring Framework.|
|Requires more manual configuration.|Automatically configures many components.|
|Often deployed as WAR files on external servers.|Runs with an embedded server like Tomcat.|
|Dependencies added individually.|Uses Starter Dependencies.|
|Longer project setup.|Quick project setup with sensible defaults.|

---

# What's Next?

Now that we've learned how Spring Boot simplifies Java backend development, we're ready to explore how multiple Spring Boot applications can work together to build scalable distributed systems.

In one of our project called Autosentry, each microservice is an independent Spring Boot application. These services communicate with one another using technologies like API Gateway, Eureka, and Kafka to form a complete microservices architecture.

Continue to **[[Microservices & Distributed Systems]]**.