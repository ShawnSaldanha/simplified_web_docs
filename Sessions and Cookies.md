
Imagine you're shopping on an online store.

You log in, add a few products to your cart, browse several pages, and finally proceed to checkout.

Despite moving through many different pages, the website somehow remembers:

- Who you are
    
- That you're logged in
    
- What's inside your shopping cart
    
- Your preferences and settings
    

But here's an interesting question.

> **How does the server remember you when every page request is completely independent?**

The answer lies in **Sessions** and **Cookies**.

---

# The Problem: HTTP is Stateless

Before understanding sessions and cookies, we first need to understand an important characteristic of HTTP.

**HTTP is a stateless protocol.**

This means that every HTTP request is treated as a completely new request.

For example,

```id="k91v3x"
GET /profile
```

A few seconds later,

```id="thiqjw"
GET /orders
```

From the server's perspective, these are simply two unrelated requests.

The server does **not automatically remember** that both requests came from the same user.

If HTTP had no mechanism for maintaining state, users would have to log in again every time they clicked a new page.

Clearly, that wouldn't make for a very good user experience.

> **Note:** If you'd like to understand what _state_ means in web applications, you can revisit [[Frontend Architecture]], where we introduced the concept of state.

---

# What is a Session?

A **session** is a way for the server to remember information about a particular user across multiple requests.

Instead of storing your login information in every request, the server creates a small record containing information such as:

- User ID
    
- Login status
    
- User role
    
- Shopping cart
    
- Other temporary information
    

This information is stored **on the server**.

For example,

```id="jlwmjlwm"
Session ID: ABC123

Stored on Server:

User ID : 15
Username : Sujith
Role : Admin
Cart : 3 Items
```

Notice that all the important information remains safely on the server.

---

# What is a Cookie?

Now another question arises.

> **If the session stays on the server, how does the browser know which session belongs to it?**

This is where **cookies** come in.

A **cookie** is a small piece of data stored inside the user's browser.

After a successful login, the server creates a session and sends back a cookie containing the **Session ID**.

```
Cookie

SessionID = ABC123
```

The browser stores this cookie automatically.

For every future request to the same website, the browser automatically sends the cookie back to the server.

```id="t84d3y"
Browser
    │
Cookie:
SessionID = ABC123
    │
    ▼
Server
```

The server looks up session **ABC123**, finds the corresponding user information, and immediately knows who made the request.

---

# Putting Everything Together

A typical login flow looks like this.

```id="xvx3ks"
User Login
      │
      ▼
Server verifies password
      │
      ▼
Create Session
(Session ID = ABC123)
      │
      ▼
Send Cookie
(SessionID = ABC123)
      │
      ▼
Browser Stores Cookie
```

Later...

```id="09hh5m"
User requests /profile
        │
Browser automatically sends

Cookie:
SessionID = ABC123
        │
        ▼
Server
        │
Looks up Session ABC123
        │
        ▼
Returns Profile
```

The user never notices any of this happening behind the scenes.

---

# Session vs Cookie

Many beginners think these are the same thing.

They are not.

|Session|Cookie|
|---|---|
|Stored on the server|Stored in the browser|
|Holds user information|Usually stores only the Session ID|
|More secure because sensitive data stays on the server|Can be viewed by the browser (though it can be protected with flags like `HttpOnly`)|
|Created and managed by the backend|Automatically stored and sent by the browser|

A simple way to remember the difference is:

> **The session stores the data. The cookie stores the key that points to that data.**

---

# Why Don't Modern APIs Always Use Sessions?

Sessions work very well.

In fact, many websites still use them today.

However, they have some limitations.

Since every logged-in user's session is stored on the server, the server must maintain this information until the user logs out or the session expires.

As applications grow and are distributed across multiple servers, managing these server-side sessions becomes more complex.

To solve this problem, many modern web applications and REST APIs use **JSON Web Tokens (JWTs)** instead of traditional sessions.

Unlike sessions, JWTs allow the client to carry proof of authentication with each request, reducing the need for the server to store session data.

We'll explore this approach in the next topic.

---

# What's Next?

Now that we understand how traditional web applications remember users across multiple requests, let's look at a modern alternative used by many APIs and single-page applications.

➡️ [[JWT (JSON Web Tokens)]]
