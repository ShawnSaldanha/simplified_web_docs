In the previous section, we learned how to create custom exceptions such as `VehicleNotFoundException`.

But creating an exception is only half the solution.

When an exception is thrown, our application still needs to decide:

- Which HTTP status code should be returned?
    
- What message should the client receive?
    
- Should the error response have a consistent format?
    

One approach is to handle every exception using `try-catch` blocks inside our controllers.

While this works, it quickly becomes repetitive as the application grows.

Spring Boot provides a much cleaner solution through **Global Exception Handling**.

---

## The Problem with `try-catch` Everywhere

Imagine our AutoSentry project has dozens of REST APIs.

Without global exception handling, every controller might look something like this:

```java
@GetMapping("/{id}")
public Vehicle getVehicle(@PathVariable Long id) {

    try {
        return vehicleService.getVehicle(id);
    } catch (VehicleNotFoundException e) {
        throw e;
    }
}
```

Now imagine writing similar `try-catch` blocks in hundreds of controller methods.

The code becomes repetitive, harder to read, and more difficult to maintain.

Our controllers should focus on handling requests—not handling errors.

---

## A Better Approach

Instead of catching exceptions inside every controller, we simply allow the exception to be thrown.

```java
@GetMapping("/{id}")
public Vehicle getVehicle(@PathVariable Long id) {
    return vehicleService.getVehicle(id);
}
```

If something goes wrong inside the service,

```java
throw new VehicleNotFoundException("Vehicle not found.");
```

Spring Boot can automatically redirect that exception to one central location.

```text
Client
   │
   ▼
Controller
   │
   ▼
Service
   │
Throws Exception
   ▼
Global Exception Handler
   │
Creates HTTP Response
   ▼
Client
```

This keeps our controllers clean while ensuring every exception is handled consistently.

---

## `@ControllerAdvice`

Spring Boot provides the `@ControllerAdvice` annotation for creating a **global exception handler**.

A class annotated with `@ControllerAdvice` watches every controller in the application.

Whenever an exception is thrown and isn't handled elsewhere, Spring Boot forwards it to this class.

```java
@ControllerAdvice
public class GlobalExceptionHandler {

}
```

Instead of every controller handling exceptions separately, one class becomes responsible for handling exceptions across the entire application.

---

## `@ExceptionHandler`

Inside the global exception handler, we use the `@ExceptionHandler` annotation.

It tells Spring Boot which method should handle a particular exception.

```java
@ExceptionHandler(VehicleNotFoundException.class)
public ResponseEntity<String> handleVehicleNotFound(
        VehicleNotFoundException ex) {

    return ResponseEntity
            .status(HttpStatus.NOT_FOUND)
            .body(ex.getMessage());
}
```

Now, whenever `VehicleNotFoundException` is thrown anywhere in our application, Spring Boot automatically calls this method.

---

## What Happens Behind the Scenes?

Let's see the complete flow.

```text
Client
    │
    ▼
GET /api/vehicles/101
    │
    ▼
Controller
    │
    ▼
Service
    │
Vehicle Not Found
    │
Throws VehicleNotFoundException
    ▼
@ControllerAdvice
    │
@ExceptionHandler
    │
Creates Error Response
    ▼
Client
```

The controller never catches the exception.

Instead, Spring Boot automatically routes the exception to the global exception handler.

---

## Returning Meaningful Responses

Instead of returning a generic server error like:

```text
500 Internal Server Error
```

we can return a response that actually explains the problem.

For example:

```json
{
  "status": 404,
  "message": "Vehicle with ID 101 was not found."
}
```

Clients now know exactly what happened and can respond appropriately.

---

## A Consistent Error Format

One major advantage of global exception handling is consistency.

Every API in the application can return errors in the same format.

For example:

```json
{
  "timestamp": "2026-07-26T18:00:00",
  "status": 404,
  "error": "Not Found",
  "message": "Vehicle with ID 101 was not found.",
  "path": "/api/vehicles/101"
}
```

Whether the request is handled by the Vehicle Service, User Service, or Notification Service, the client receives a predictable response structure.

This makes frontend development much easier because every error response follows the same format.

---

## Benefits of Global Exception Handling

Using a global exception handler provides several advantages:

- Eliminates repetitive `try-catch` blocks.
    
- Keeps controllers focused on business logic.
    
- Returns consistent error responses across the application.
    
- Makes the code easier to maintain.
    
- Simplifies debugging and future enhancements.
    

This is why almost every production Spring Boot application uses centralized exception handling.

---

## Exception Handling in AutoSentry

In our AutoSentry project, each microservice is an independent Spring Boot application.

Every service maintains its own global exception handler.

For example:

```text
Vehicle Service
    │
    └── GlobalExceptionHandler

User Service
    │
    └── GlobalExceptionHandler

Notification Service
    │
    └── GlobalExceptionHandler
```

This allows every microservice to handle its own exceptions while maintaining a consistent API experience for clients.

---

## Key Takeaways

- `@ControllerAdvice` creates a centralized exception handling class.
    
- `@ExceptionHandler` specifies how individual exceptions should be handled.
    
- Controllers remain focused on processing requests instead of handling errors.
    
- Global exception handling produces consistent HTTP responses across the application.
    
- Centralized exception handling is a standard practice in Spring Boot applications.
    

---

# What's Next?

Now that we've learned how to build robust Spring Boot applications with centralized exception handling, we're ready to take the next step: breaking a single application into multiple independent services.

In our **AutoSentry** project, each microservice is an independent Spring Boot application. These services communicate with one another using technologies like API Gateway, Eureka, and Kafka to form a complete microservices architecture.

Continue to **[[Microservices & Distributed Systems]]**.