Imagine you have spent months building a beautiful web application. Users can sign up, log in, upload photos, make payments, and store personal information. Now imagine if anyone on the internet could simply pretend to be another user, read someone else's data, or steal passwords with a few carefully crafted requests.

This is exactly why **web security** exists.

Security is not a single feature that you add at the end of a project. It is a collection of techniques and best practices that protect your application, your users, and your data from unauthorized access and malicious attacks.

Whether you're building a simple blog or a large-scale social media platform, every web application needs to answer a few important questions:

- **Who is the user?**
    
- **How do we verify their identity?**
    
- **What resources are they allowed to access?**
    
- **How do we safely store sensitive information like passwords?**
    
- **How do we ensure data cannot be intercepted while travelling across the internet?**
    
- **How do we prevent attackers from manipulating our application?**

Throughout this section, you'll learn how modern web applications answer these questions using authentication systems, secure password storage, encrypted communication, and several other security mechanisms that are used in almost every real-world application.

---

# The Big Picture

A simplified login flow of a secure web application usually looks like this:

```
User
   │
   │ Login Request
   ▼
Backend Server
   │
   ├── Verify username & password
   ├── Compare hashed passwords
   ├── Generate authentication token/session
   ▼
User receives proof of authentication
   │
   │
Future Requests
   │
   ├── Include token or session information
   ▼
Backend verifies identity
   │
   ▼
Allow or deny access
```

Behind this simple flow are several different technologies working together.

For example:

- Passwords are **hashed** before being stored in the database.
    
- Authentication tokens such as **JWTs** help identify users after they log in.
    
- **HTTPS** encrypts communication between the browser and the server.
    
- **CORS** controls which websites are allowed to communicate with your backend.
    
- **OAuth** allows users to log in using services like Google or GitHub.
    
- Secure database practices help prevent attacks such as **SQL Injection**.

Each of these concepts solves a different security problem, and together they create a secure web application.

---

# Topics Covered

This section is divided into the following topics:

- [[Authentication vs Authorization]] – Understanding the difference between verifying a user's identity and deciding what they are allowed to do.
    
- [[Password Hashing]] – Why passwords should never be stored in plain text and how modern applications protect them.
    
- [[Sessions and Cookies]] – How web applications remember users after they log in.
    
- [[JWT (JSON Web Tokens)]] – A modern approach to stateless authentication used by many APIs and web applications.
    
- [[HTTPS & SSL-TLS]] – How encryption protects data while it travels across the internet.
    
- [[CORS]] – Understanding why browsers block certain cross-origin requests and how servers allow trusted clients.
    
- [[OAuth 2.0 & Social Login]] – How applications let users sign in with services like Google or GitHub without sharing passwords.
