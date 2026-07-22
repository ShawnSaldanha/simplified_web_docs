If you've completed the [[Core Java Concepts]], you now know that Java is a powerful language capable of building almost any type of application. In theory, we could build an entire web application using only plain Java.

So why don't most companies do that?

As applications grow larger, writing everything from scratch quickly becomes repetitive, difficult to maintain, and harder to scale. Developers found themselves solving the same problems over and over again—creating objects, managing dependencies, configuring databases, handling transactions, and much more.

The **Spring Framework** was created to solve these common problems, allowing developers to focus on writing business logic instead of repetitive infrastructure code.

---

# What is a Framework?

Before understanding Spring, let's first understand what a framework is.

A **library** provides tools that your application can use whenever you choose.

A **framework** provides the overall structure of your application and controls how different parts work together.

Think of building a house.

If Java is like having individual construction tools (hammer, saw, drill), then Spring is like having an experienced architect who already provides the blueprint for building the house correctly.

Instead of deciding how everything should connect together yourself, Spring provides a well-tested structure that developers can build upon.

---

# The Problem with Plain Java

Imagine we're building a simple application for AutoSentry.

We have two classes:

```java
public class NotificationService {

    public void sendEmail() {
        System.out.println("Email sent!");
    }

}
```

```java
public class VehicleService {

    private NotificationService notificationService =
            new NotificationService();

}
```

This works perfectly.

But imagine our application grows to hundreds of classes.

```text
VehicleService
        │
        ▼
NotificationService
        │
        ▼
EmailService
        │
        ▼
TemplateService
        │
        ▼
DatabaseService
```

Every class keeps creating more objects using the `new` keyword.

This creates several problems:

- Classes become tightly connected.
    
- Replacing one implementation often requires changing many files.
    
- Testing becomes difficult.
    
- Managing object creation becomes repetitive.
    

There had to be a better solution.

---

# The Spring Way

Instead of every class creating its own objects, Spring creates and manages those objects for us.

Rather than saying,

```java
NotificationService notificationService =
        new NotificationService();
```

we simply tell Spring:

> "Whenever I need a NotificationService, please provide one."

Spring takes responsibility for creating the object and giving it to us whenever it's needed.

This idea is called **Dependency Injection**.

---

# What is Dependency Injection?

A **dependency** is simply another object that a class needs to do its job.

For example,

```text
VehicleService
        │
needs
        ▼
NotificationService
```

Here,

`NotificationService`

is a dependency of

`VehicleService`.

Instead of creating the dependency ourselves,

Spring injects it into our class automatically.

```text
Spring Container
        │
        │ creates
        ▼
NotificationService
        │
        │ injects
        ▼
VehicleService
```

This keeps our classes independent and much easier to maintain.

---

# Inversion of Control (IoC)

Dependency Injection is made possible because of another concept called **Inversion of Control**, often shortened to **IoC**.

Without Spring:

```text
VehicleService
        │
creates
        ▼
NotificationService
```

With Spring:

```text
Spring
      │
creates
      ▼
NotificationService
      │
gives to
      ▼
VehicleService
```

Notice what changed.

The responsibility of creating objects moved **from our code to Spring**.

This reversal of responsibility is called **Inversion of Control**.

---

# The IoC Container

Now you might be wondering,

> If our classes don't create objects anymore, who does?

The answer is the **Spring IoC Container**.

Think of it as a large warehouse that stores all the objects used by our application.

```text
        Spring IoC Container

     ┌─────────────────────┐
     │ NotificationService │
     │ UserService         │
     │ VehicleService      │
     │ EmailService        │
     │ JwtService          │
     └─────────────────────┘
```

Whenever an object is required,

Spring simply retrieves it from this container instead of creating a new one every time.

---

# What is a Bean?

Any object that is created and managed by the Spring IoC Container is called a **Spring Bean**.

For example,

```text
NotificationService
```

becomes a Bean.

```text
VehicleService
```

also becomes a Bean.

Spring creates these objects when the application starts and manages their entire lifecycle.

---

# Common Spring Annotations

Spring identifies different types of Beans using annotations.

### `@Component`

A general-purpose Spring-managed class.

```java
@Component
public class EmailService {

}
```

---

### `@Service`

Used for classes containing business logic.

```java
@Service
public class VehicleService {

}
```

---

### `@Repository`

Used for database-related classes.

```java
@Repository
public class VehicleRepository {

}
```

---

### `@Controller`

Used to handle incoming HTTP requests.

```java
@Controller
public class VehicleController {

}
```

(When building REST APIs, you'll usually use `@RestController`, which we'll cover in the Spring Boot section.)

---

# Injecting Dependencies

Instead of creating objects ourselves,

```java
NotificationService service =
        new NotificationService();
```

Spring can inject them.

The recommended approach is **constructor injection**.

```java
@Service
public class VehicleService {

    private final NotificationService notificationService;

    public VehicleService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }

}
```

Spring automatically creates the `NotificationService` Bean and passes it into the constructor.

No `new` keyword required.

---

# Why is this Better?

Using Spring provides several advantages:

- Less repetitive code.
    
- Loose coupling between classes.
    
- Easier testing.
    
- Easier maintenance.
    
- Better scalability.
    
- Built-in support for many enterprise features.
    

Instead of worrying about object creation, we can focus on solving business problems.

---

# Spring vs Plain Java

|Plain Java|Spring Framework|
|---|---|
|We create objects manually.|Spring manages object creation.|
|Heavy use of the `new` keyword.|Dependencies are injected automatically.|
|Tight coupling between classes.|Loose coupling using Dependency Injection.|
|More configuration and boilerplate.|Much cleaner and easier to maintain.|

---

# Is Spring Enough?

The Spring Framework solved many problems faced by Java developers, but configuring Spring projects was still time-consuming.

Developers had to configure dependencies, web servers, application settings, and many other components manually before writing any business logic.

To simplify this even further, the Spring team introduced **Spring Boot**, which automates much of this configuration and allows developers to start building applications much faster.

---

# What's Next?

Now that we understand why the Spring Framework exists and how it manages our application's objects, the next step is learning how **Spring Boot** simplifies Spring development even further.

In the next section, we'll explore:

- Why Spring Boot was introduced
    
- Auto Configuration
    
- Starter Dependencies
    
- Embedded Web Servers
    
- How we built our AutoSentry microservices using Spring Boot
    

Continue to [[Spring Boot]].