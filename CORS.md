
Imagine you're building a web application.

Your frontend is running at:

```text
http://localhost:3000
```

and your backend API is running at:

```text
http://localhost:8080
```

Your frontend tries to fetch user information.

```javascript
fetch("http://localhost:8080/api/users");
```

Instead of receiving the expected response, the browser displays an error similar to:

```text
Access to fetch at 'http://localhost:8080'
has been blocked by CORS policy.
```

But why?

Both applications belong to you.

The answer lies in a browser security mechanism called **CORS (Cross-Origin Resource Sharing).**

---

# Understanding an Origin

Before understanding CORS, we first need to understand what an **Origin** is.

An **Origin** is defined by three components:

- Protocol (HTTP or HTTPS)
    
- Domain (example.com)
    
- Port (80, 443, 3000, etc.)
    

For example,

|URL|Origin|
|---|---|
|`https://example.com`|`https + example.com + 443`|
|`http://localhost:3000`|`http + localhost + 3000`|
|`http://localhost:8080`|`http + localhost + 8080`|

Even though both URLs use **localhost**, these are considered **different origins** because their ports are different.

---

# Same-Origin Policy

Browsers enforce an important security rule called the **Same-Origin Policy (SOP).**

By default, JavaScript running on one origin is **not allowed** to freely access resources from another origin.

For example,

```text
Frontend

http://localhost:3000
```

trying to access

```text
http://localhost:8080
```

is considered a **cross-origin request**.

Without additional permission, the browser blocks it.

---

# Why Does This Rule Exist?

Imagine you are logged into your online banking account.

Now suppose you accidentally visit a malicious website.

Without the Same-Origin Policy, that malicious website could silently make requests to your bank using your existing login session and potentially access sensitive information.

The Same-Origin Policy prevents websites from freely interacting with resources belonging to other origins, making many attacks significantly more difficult.

---

# So What is CORS?

CORS stands for **Cross-Origin Resource Sharing**.

It is a mechanism that allows a server to tell the browser:

> **"I trust requests coming from this particular origin."**

For example,

Suppose your frontend runs at:

```text
http://localhost:3000
```

Your backend can respond with the following HTTP header:

```http
Access-Control-Allow-Origin: http://localhost:3000
```

Now the browser sees:

> "The server explicitly allows this origin."

The request is therefore allowed.

Without this header, the browser blocks access to the response.

---

# How CORS Works

Let's look at the complete flow.

```text
Browser
      │
Request to Backend
      │
      ▼
Backend
      │
Returns:
Access-Control-Allow-Origin:
http://localhost:3000
      │
      ▼
Browser checks the header
      │
      ├── Allowed ✔
      └── Not Allowed ✖
```

Notice something important:

The **server does not enforce CORS.**

The **browser** does.

The server simply tells the browser what is allowed.

---

# CORS Does Not Stop Server-to-Server Requests

Many beginners think CORS protects the backend from every request.

It does not.

Suppose another backend server sends a request.

```text
Backend A
      │
HTTP Request
      ▼
Backend B
```

There is no browser involved.

Since CORS is a browser security feature, this request is allowed.

Similarly, tools like:

- Postman
    
- curl
    
- Insomnia
    

can send requests without being affected by CORS.

This is why APIs can still be tested even if CORS is not configured.

---

# Simple Requests and Preflight Requests

Not every request is handled in the same way.

Some requests are considered **simple requests** and are sent directly.

However, requests involving:

- `PUT`
    
- `PATCH`
    
- `DELETE`
    
- custom headers (such as `Authorization`)
    
- certain content types
    

usually trigger a **preflight request**.

Before sending the actual request, the browser first sends an `OPTIONS` request asking:

> "Is it okay if I send this request?"

If the server approves, the browser proceeds with the real request.

Otherwise, the browser blocks it.

---

# Example

```text
Browser

OPTIONS /api/users
```

Server responds:

```http
Access-Control-Allow-Origin: http://localhost:3000
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Headers: Authorization
```

The browser now knows the request is permitted and sends the actual API request.

---

# CORS in Development

When building web applications locally, it's common to have:

Frontend:

```text
http://localhost:3000
```

Backend:

```text
http://localhost:8080
```

Since these are different origins, developers usually configure the backend to allow requests from the frontend during development.

In production, this is often restricted to the application's actual domain.

---

# The Big Picture

```text
Frontend
(http://localhost:3000)
        │
        │ Request
        ▼
Backend
(http://localhost:8080)
        │
        │
Returns:
Access-Control-Allow-Origin
        │
        ▼
Browser
        │
Checks Permission
        │
        ├── Allowed ✔
        └── Blocked ✖
```

---

# Common Misconceptions

|Myth|Reality|
|---|---|
|CORS is enforced by the backend.|❌ The browser enforces CORS.|
|CORS blocks Postman requests.|❌ Postman is not affected by CORS.|
|CORS is an authentication mechanism.|❌ It only controls which browser origins can access responses.|
|Two localhost URLs always have the same origin.|❌ Different ports create different origins.|

---

# What's Next?

So far, we've explored how browsers securely communicate with backend servers and how they control which websites are allowed to access resources using **CORS**.

The next question is:

> **How can websites let users sign in with their Google or GitHub accounts without ever asking for their passwords?**

We'll answer that in the next topic:

➡️ [[OAuth 2.0 & Social Login]]