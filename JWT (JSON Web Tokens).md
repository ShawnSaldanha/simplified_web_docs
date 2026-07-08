
In the previous topic, we learned how **sessions** allow a server to remember users after they log in.

Sessions have been used successfully for many years and are still widely used today.

However, as web applications became larger and started running on multiple servers, managing sessions became increasingly difficult.

This led to another question:

> **Can we authenticate users without storing their session on the server?**

One popular solution is **JWT (JSON Web Token)**.

JWT allows the server to verify a user's identity without maintaining session data for every logged-in user. Instead, the client carries proof of authentication with every request.

This approach is called **stateless authentication**.

---

# Why Were JWTs Introduced?

Imagine a large social media platform with millions of users.

Instead of having one backend server, the application now runs on hundreds of servers.

```
                 Internet
                     │
                     ▼
              Load Balancer
           ┌──────┼──────┐
           ▼      ▼      ▼
       Server A Server B Server C
```

Suppose you log in through **Server A**.

If traditional sessions are being used, your session information exists only on Server A.

Now your next request is routed to **Server C**.

```
Login
   │
   ▼
Server A
(Session Stored Here)

Next Request
      │
      ▼
Server C
```

Server C has no idea who you are because your session is stored elsewhere.

To solve this problem, developers often need additional infrastructure like shared session stores (for example, Redis) or sticky sessions, which adds complexity.

JWT takes a different approach.

Instead of storing user information on the server, the server sends the client a **signed token** containing the information required to identify the user.

The client simply sends this token back with every future request.

---

# How JWT Authentication Works

Let's see the complete login process.

### Step 1 — User Logs In

The user enters their credentials.

```
Email
Password
```

The browser sends these credentials to the backend.

---

### Step 2 — Backend Verifies Credentials

The backend:

- Finds the user
    
- Compares the hashed password
    
- Successfully authenticates the user
    

At this point, the backend knows the user's identity.

---

### Step 3 — Server Creates a JWT

Instead of creating a server-side session, the backend creates a JWT.

A JWT usually contains information like:

```json
{
    "userId": 15,
    "username": "Sujith",
    "role": "ADMIN"
}
```

This information is called the **payload**.

The server then signs the token using its **secret key**.

This signature ensures that the token cannot be modified without being detected.

---

### Step 4 — Server Sends JWT to the Client

```
Backend
    │
    ▼
JWT Token
```

The browser stores this token.

It may be stored in:

- Local Storage
    
- Session Storage
    
- An HTTP-only Cookie
    

depending on how the application is designed.

---

### Step 5 — Future Requests

Whenever the client sends another request, it includes the JWT.

```
GET /profile

Authorization:
Bearer eyJhbGciOi...
```

The server verifies the token using the same secret key that was used to sign it.

If the signature is valid, the request is accepted.

Otherwise, it is rejected.

Notice that the server never needed to look up any session information.

Everything required to identify the user came from the JWT itself.

---

# The Structure of a JWT

A JWT consists of three parts separated by dots.

```
Header.Payload.Signature
```

For example,

```
xxxxx.yyyyy.zzzzz
```

Each part has a specific purpose.

---

## 1. Header

The header contains metadata about the token.

For example:

```json
{
    "alg": "HS256",
    "typ": "JWT"
}
```

It tells the server:

- which signing algorithm was used
    
- that this token is a JWT
    

---

## 2. Payload

The payload contains information about the user.

For example,

```json
{
    "userId": 15,
    "username": "Sujith",
    "role": "ADMIN"
}
```

These pieces of information are called **claims**.

The payload is **encoded**, **not encrypted**.

This means anyone who has the token can read its contents.

Therefore,

> **Never store sensitive information such as passwords inside a JWT.**

---

## 3. Signature

The signature is generated using

- the Header
    
- the Payload
    
- the server's Secret Key
    

```
Header
Payload
Secret Key
      │
      ▼
Generate Signature
```

If anyone changes even a single character in the Header or Payload, the generated signature changes completely.

When the server receives a JWT, it generates the signature again using its secret key.

If both signatures match, the token is genuine.

Otherwise, the request is rejected.

---

# Why Can't Someone Modify the JWT?

Suppose someone changes

```json
{
    "role": "USER"
}
```

to

```json
{
    "role": "ADMIN"
}
```

Although modifying the payload is easy, the attacker **cannot generate a valid signature** because they do not know the server's secret key.

When the server verifies the JWT, the signatures won't match, and the request is immediately rejected.

This is why the server's **secret key must always remain private**.

---

# JWT vs Sessions

|Sessions|JWT|
|---|---|
|Server stores session data|Client stores the token|
|Browser usually stores only the Session ID|Browser stores the JWT|
|Server must remember every logged-in user|Server only verifies the token|
|Stateful Authentication|Stateless Authentication|
|Common in traditional web applications|Common in REST APIs and Single Page Applications|

Neither approach is universally better.

Many applications still use sessions, while many modern APIs prefer JWTs because they simplify authentication across distributed systems.

---

# Token Expiration

JWTs are usually created with an expiration time.

For example,

```
Valid for 15 minutes
```

or

```
Valid for 1 hour
```

After the expiration time, the token is no longer accepted.

This limits the damage if a token is accidentally exposed.

Many applications also use **Refresh Tokens** to obtain new access tokens without requiring the user to log in again.

---

# The Big Picture

```
User Logs In
      │
      ▼
Backend Verifies Password
      │
      ▼
Create JWT
      │
      ▼
Send JWT to Client
      │
      ▼
Client Stores JWT
      │
      ▼
Future Requests
Authorization: Bearer <JWT>
      │
      ▼
Backend Verifies Signature
      │
      ▼
Allow or Deny Access
```

---

# What's Next?

Authentication ensures that only legitimate users can access your application.

However, even if the user is authenticated, the communication between the browser and the server still travels across the internet.

How do we prevent attackers from reading or modifying that data while it's in transit?

We'll answer that in the next topic:

➡️ [[HTTPS & SSL-TLS]]
