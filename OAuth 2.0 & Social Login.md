
So far, we've learned how users typically create an account by choosing a username, email, and password.

The application stores a hashed version of the password, verifies it during login, and then authenticates the user using a session or a JWT.

However, many modern websites also provide options like:

- Continue with Google
    
- Continue with GitHub
    
- Continue with Facebook
    
- Sign in with Microsoft
    

This raises an interesting question.

> **If I click "Continue with Google", does that website receive my Google password?**

The answer is **no**.

Instead of sharing your password with every application you use, websites rely on a standard protocol called **OAuth 2.0**.

OAuth allows one application to securely obtain limited information from another application **without ever seeing your password**.

---

# Why Do We Need OAuth?

Imagine a new website asks you to log in using your Google account.

Without OAuth, the website would have to ask for your Google password directly.

```text
New Website

Google Email:
Google Password:
```

This would be extremely dangerous because:

- The website could store your password.
    
- It could misuse your account.
    
- You would need to trust every website with your credentials.
    

OAuth eliminates this problem.

Instead of giving your password to the website, you authenticate directly with Google.

Google then tells the website:

> "Yes, this user has successfully logged in."

The website never learns your Google password.

---

# How Social Login Works

Let's look at the overall flow.

### Step 1 — User Chooses Google Login

Instead of entering a password, the user clicks:

```text
Continue with Google
```

---

### Step 2 — Browser is Redirected

The application redirects the user to Google's login page.

Notice something important.

The login page belongs to:

```text
accounts.google.com
```

Your application never displays or handles your Google password.

---

### Step 3 — User Authenticates with Google

The user enters their Google credentials.

Google verifies the login.

If successful, Google asks the user whether they want to share certain information with the application.

For example:

- Name
    
- Email Address
    
- Profile Picture
    

The user can then approve or deny this request.

---

### Step 4 — Google Returns an Authorization Code

If the user grants permission, Google redirects the browser back to your application with a temporary **Authorization Code**.

This code is **not** the user's password.

It is simply proof that the user successfully authenticated with Google and approved the requested permissions.

---

### Step 5 — Backend Contacts Google

Your backend sends the Authorization Code to Google.

Google verifies the code and returns an **Access Token**.

Using this token, your backend can retrieve the user's basic profile information.

For example:

```json
{
    "name": "Sujith Kumar",
    "email": "sujith@gmail.com",
    "picture": "..."
}
```

Your application can now create or log in the user without ever knowing their Google password.

---

# The Complete Flow

```text
User
   │
Click "Continue with Google"
   │
   ▼
Application
   │
Redirect
   ▼
Google Login Page
   │
User Logs In
   │
Permission Granted
   ▼
Authorization Code
   │
   ▼
Application Backend
   │
Exchange Code
   ▼
Google
   │
Access Token
   ▼
User Information
   │
Create/Login User
```

---

# OAuth vs Traditional Login

|Traditional Login|OAuth Login|
|---|---|
|User creates a password|No password is created for your application|
|Application stores a hashed password|Password remains with Google (or another provider)|
|Application verifies credentials|Google verifies the user's identity|
|Application generates its own JWT/session after login|Application usually still generates its own JWT/session after successful OAuth login|

Notice the last point.

Even after Google authenticates the user, **your application still usually creates its own session or JWT** so the user can interact with your application normally.

OAuth replaces the **authentication step**, not your application's own authorization or session management.

---

# OAuth is About Authorization

The name **OAuth** stands for **Open Authorization**.

Although it's commonly used for social login, OAuth was originally designed to let users grant limited access to their data without sharing passwords.

For example, you might allow a photo-editing application to access your Google Photos or a calendar application to read your Google Calendar.

The user chooses exactly what permissions to grant, and those permissions can be revoked later without changing their Google password.

---

# The Big Picture

```text
User
   │
Click "Continue with Google"
   ▼
Google Authenticates User
   │
Returns Authorization Code
   ▼
Backend Exchanges Code for Access Token
   │
Gets User Information
   ▼
Creates Local User (if needed)
   │
Generates JWT / Session
   ▼
User Logged In
```

---

# Where to Go Next?

Congratulations! 🎉

You've now covered the core security concepts that every web developer encounters while building modern web applications:

- Authentication vs Authorization
    
- Password Hashing
    
- Sessions and Cookies
    
- JWT
    
- HTTPS & SSL/TLS
    
- CORS
    
- OAuth 2.0 & Social Login
    

These concepts work together to ensure that users can securely authenticate, communicate with servers safely, and access only the resources they're permitted to use.
