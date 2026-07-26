In the previous section, we learned that Java provides many built-in exception classes like `NullPointerException`, `IOException`, and `IllegalArgumentException`.

While these exceptions are useful, they often don't describe **business-specific problems** in our application.

For example, imagine our AutoSentry application.

If a client requests a vehicle that doesn't exist, should we throw a generic exception like this?

```java
throw new RuntimeException("Something went wrong.");
```

Technically, yes.

But does it clearly explain the problem?

Not really.

Instead, we can create an exception that represents exactly what happened.

```java
throw new VehicleNotFoundException("Vehicle not found.");
```

The second approach is much more meaningful.

This is the purpose of **custom exceptions**.

---

## Why Do We Need Custom Exceptions?

Every application has its own business rules.

For example, in AutoSentry:

- A vehicle may not exist.
    
- A user may already be registered.
    
- An insurance policy may have expired.
    
- A notification may fail to send.
    

None of these situations are represented by Java's built-in exceptions.

Instead of repeatedly using generic exceptions, we create our own exception classes that clearly describe the business problem.

This makes the code easier to understand for both current and future developers.

---

## Creating a Custom Exception

Creating a custom exception is straightforward.

We simply create a class that extends one of Java's exception classes.

In most Spring Boot applications, custom exceptions extend `RuntimeException`.

```java
public class VehicleNotFoundException extends RuntimeException {

    public VehicleNotFoundException(String message) {
        super(message);
    }
}
```

Now we have an exception whose name immediately explains the problem.

---

## Using a Custom Exception

Once we've created the exception, we can throw it whenever the situation occurs.

For example:

```java
if (vehicle == null) {
    throw new VehicleNotFoundException("Vehicle not found.");
}
```

Execution flow:

```text
Client Request
      │
      ▼
Search Vehicle
      │
Vehicle Found?
 ├── Yes ─────► Return Vehicle
 │
 └── No
       │
       ▼
Throw VehicleNotFoundException
```

Notice how the exception itself tells us exactly what happened.

---

## Why Not Just Use RuntimeException?

Suppose we have this code:

```java
throw new RuntimeException("Something went wrong.");
```

Now compare it with:

```java
throw new VehicleNotFoundException("Vehicle not found.");
```

Which one is easier to understand?

The second one.

A developer reading the code immediately knows:

- What failed.
    
- Why it failed.
    
- Which part of the application caused the problem.
    

Meaningful exception names make the code almost self-explanatory.

---

## Common Custom Exceptions

As applications grow, it's common to have many custom exceptions.

For example, our AutoSentry project might include:

```text
VehicleNotFoundException

UserAlreadyExistsException

InsuranceExpiredException

NotificationFailedException

InvalidRegistrationNumberException
```

Each exception represents a specific business scenario.

Instead of one generic exception trying to describe every problem, each exception focuses on a single responsibility.

---

## Benefits of Custom Exceptions

Creating custom exceptions provides several advantages:

- Makes the code easier to read.
    
- Clearly represents business rules.
    
- Makes debugging simpler.
    
- Allows different errors to be handled differently.
    
- Improves the maintainability of large applications.
    

As a project grows from a few classes to hundreds of classes, these benefits become even more valuable.

---

## How Are Custom Exceptions Handled?

Creating a custom exception is only the first step.

When we throw an exception, we still need a way to convert it into a meaningful response for the client.

One approach is to write `try-catch` blocks everywhere, but that quickly becomes repetitive and difficult to maintain.

A better approach is to let Spring Boot handle exceptions from one central place.

```text
Controller
     │
     ▼
Service
     │
Throws VehicleNotFoundException
     ▼
Global Exception Handler
     │
Creates HTTP Response
     ▼
Client
```

We'll learn how Spring Boot does this in the next section.

---

## Key Takeaways

- Java's built-in exceptions don't cover every business scenario.
    
- Custom exceptions allow us to represent application-specific problems.
    
- Most Spring Boot applications create custom exceptions by extending `RuntimeException`.
    
- Meaningful exception names improve readability and maintainability.
    
- Custom exceptions become even more powerful when combined with centralized exception handling.
    

---

## What's Next?

We've learned how to create exceptions that clearly represent business-specific problems.

Now we'll see how Spring Boot catches these exceptions in one central location and converts them into consistent HTTP responses using `@ControllerAdvice` and `@ExceptionHandler`.

Continue to **[[Global Exception Handling (Spring Boot)]]**.