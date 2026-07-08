
Imagine you walk into a college library.

The librarian first asks to see your college ID card. Once they verify that the ID belongs to you, they allow you to enter the library.

However, entering the library doesn't mean you can access everything inside. Certain rooms, such as the server room or staff office, are restricted to authorized personnel only.

This simple example demonstrates two different security concepts used in almost every web application.

- **Authentication** answers the question:
    
    > **"Who are you?"**
    
- **Authorization** answers the question:
    
    > **"What are you allowed to do?"**
    

Although these terms are often used together, they solve two completely different problems.

---

# Authentication – Proving Your Identity

Authentication is the process of verifying that a user is really who they claim to be.

Whenever you log into an application, the system needs some way to confirm your identity before granting access.

Common authentication methods include:

- Username and Password
    
- Email and Password
    
- Mobile Number with OTP
    
- Fingerprint or Face ID
    
- Login with Google or GitHub (OAuth)
    

For example, when you enter your email and password on a website:

1. Your browser sends the login request to the backend.
    
2. The backend searches for your account.
    
3. It verifies whether the submitted password matches the securely stored password.
    
4. If everything is correct, the backend considers you **authenticated**.
    

At this stage, the server knows **who you are**, but it still hasn't decided **what you're allowed to do**.

---

# Authorization – Determining Permissions

Once the user's identity has been verified, the application must decide what actions that user is permitted to perform.

This process is called **authorization**.

Different users often have different permissions within the same application.

Consider an online shopping platform:

|User|Allowed Actions|
|---|---|
|Customer|Browse products, place orders, view personal profile|
|Seller|Add products, manage inventory, process orders|
|Administrator|Manage users, products, reports, and system settings|

All three users successfully log in.

However, they should not all have the same level of access.

A customer should never be able to delete products from the database, just as a seller should not be able to manage administrator accounts.

Authorization ensures that each user can perform only the actions assigned to their role.

---

# Authentication Always Comes First

A web application typically performs these steps whenever a user accesses a protected resource.

```
User
   │
   │ Login
   ▼
Authentication
   │
   │ Identity Verified
   ▼
Authorization
   │
   │ Check Permissions
   ▼
Allow or Deny Access
```

Without authentication, the server doesn't even know who the user is.

Without authorization, every authenticated user would have unrestricted access to every part of the application.

Both processes are essential for maintaining application security.

---

# A Real-World Example

Imagine you're using an online banking application.

When you log in with your username and password:

- The bank verifies your credentials.
    
- You are successfully **authenticated**.
    

Now suppose you try to access another customer's account by manually changing the account number in the URL.

Even though you're authenticated, the server checks whether you have permission to access that account.

Since you don't, the request is rejected.

This is **authorization** protecting sensitive data.

---

# Authentication vs Authorization

|Authentication|Authorization|
|---|---|
|Verifies the user's identity|Determines what the user is allowed to do|
|Happens first|Happens after authentication|
|Answers "Who are you?"|Answers "What can you access?"|
|Usually involves passwords, OTPs, biometrics, or OAuth|Usually involves roles, permissions, or access rules|
|Example: Logging into Gmail|Example: Only administrators can delete users|

---

# What's Next?

Now that we understand how a web application identifies users and controls their permissions, the next question is:

> **How does the server securely store a user's password without saving the actual password?**

We'll answer that in the next topic:

➡️ [[Password Hashing]]
