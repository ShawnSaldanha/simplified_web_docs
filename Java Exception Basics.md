In the previous section, we learned why exception handling is important. Now let's understand how Java helps us deal with unexpected situations using its built-in exception handling mechanism.

Whenever something unexpected happens while a Java program is running, Java creates an **exception**. If we don't handle it, the program may stop executing, and the exception details are displayed.

Fortunately, Java provides several keywords that allow us to detect, handle, and even create exceptions.

---

## What is an Exception?

An **exception** is an object that represents an unexpected event occurring during the execution of a program.

For example, consider the following code:

```java
int result = 10 / 0;
```

Since we cannot divide a number by zero, Java throws an exception.

```
Exception in thread "main"
java.lang.ArithmeticException: / by zero
```

Instead of allowing the program to terminate unexpectedly, we can handle this situation.

---

## The `try` and `catch` Blocks

The most common way to handle an exception is using `try` and `catch`.

The code that might produce an exception is placed inside the `try` block.

If an exception occurs, Java immediately stops executing the remaining code inside the `try` block and transfers control to the matching `catch` block.

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero.");
}
```

Execution flow:

```text
Start
  │
  ▼
try Block
  │
Exception?
 ├── No ─────────► Continue Normally
 │
 └── Yes
       │
       ▼
   catch Block
       │
       ▼
Continue Program
```

Instead of crashing, the program handles the problem and continues executing.

---

## The `finally` Block

Sometimes we have code that should always run, whether an exception occurs or not.

This code is placed inside the `finally` block.

```java
try {
    System.out.println("Opening database connection...");
} catch (Exception e) {
    System.out.println("Something went wrong.");
} finally {
    System.out.println("Closing database connection.");
}
```

The `finally` block is commonly used for cleanup tasks, such as:

- Closing database connections
    
- Closing files
    
- Releasing resources
    

Its code executes regardless of whether an exception was thrown.

```text
try
 │
 ▼
Exception?
 ├── No ───────► finally
 │
 └── Yes
      │
      ▼
   catch
      │
      ▼
   finally
```

---

## The `throw` Keyword

Sometimes we want to create an exception ourselves.

Java allows us to do this using the `throw` keyword.

```java
if (age < 18) {
    throw new IllegalArgumentException("Age must be at least 18.");
}
```

Here, we are explicitly telling Java that this situation should be treated as an error.

This is useful when enforcing business rules in our applications.

---

## The `throws` Keyword

The `throws` keyword is different from `throw`.

Instead of creating an exception, it tells Java that a method may produce an exception and leaves the responsibility of handling it to the method that calls it.

```java
public void readFile() throws IOException {
    // File reading logic
}
```

Think of it as saying:

> "This method might encounter an exception. Whoever calls this method should be prepared to handle it."

---

## Checked vs Unchecked Exceptions

Java classifies exceptions into two main categories.

### Checked Exceptions

Checked exceptions are verified by the Java compiler.

The compiler requires us to either handle them using `try-catch` or declare them using `throws`.

Examples include:

- `IOException`
    
- `SQLException`
    

---

### Unchecked Exceptions

Unchecked exceptions are **not** checked by the compiler.

These usually occur because of programming mistakes or invalid data during runtime.

Examples include:

- `NullPointerException`
    
- `ArithmeticException`
    
- `IllegalArgumentException`
    
- `ArrayIndexOutOfBoundsException`
    

In backend development, most custom exceptions extend `RuntimeException`, making them unchecked exceptions.

---

## Bringing Everything Together

The following example demonstrates several concepts together.

```java
try {
    int age = 15;

    if (age < 18) {
        throw new IllegalArgumentException("Age must be at least 18.");
    }

    System.out.println("Access Granted.");

} catch (IllegalArgumentException e) {
    System.out.println(e.getMessage());
} finally {
    System.out.println("Request Finished.");
}
```

Execution flow:

```text
try
 │
 ▼
Business Rule Check
 │
 ▼
Exception?
 ├── No ─────► Success
 │
 └── Yes
      │
      ▼
throw
      │
      ▼
catch
      │
      ▼
finally
```

This demonstrates how Java detects an exception, transfers control to the `catch` block, and finally executes the cleanup code.

---

## Key Takeaways

- An exception represents an unexpected event during program execution.
    
- `try` contains code that might produce an exception.
    
- `catch` handles exceptions and prevents the program from terminating unexpectedly.
    
- `finally` executes whether an exception occurs or not.
    
- `throw` is used to create an exception.
    
- `throws` declares that a method may produce an exception.
    
- Java exceptions are broadly classified into checked and unchecked exceptions.
    

---

## What's Next?

Java already provides many built-in exception classes. However, real-world applications often need exceptions that represent specific business scenarios.

For example, in our AutoSentry project, a missing vehicle is different from a missing user, and both should communicate meaningful information to the client.

In the next section, we'll learn how to create our own exception classes and understand why **custom exceptions** make our applications cleaner, more expressive, and easier to maintain.

Continue to **[[Custom Exceptions]]**.