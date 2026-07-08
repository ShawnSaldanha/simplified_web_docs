
Imagine you create an account on a new website using the password:

```
MySecret@123
```

You probably expect the website to remember your password so that it can verify it the next time you log in.

But here's an important question:

> **Does the website actually store your password exactly as you typed it?**

Thankfully, **no**.

If websites stored passwords in plain text, anyone who gained access to the database—including hackers or even malicious employees—could immediately see every user's password.

This is why modern web applications never store the original password. Instead, they store something called a **hash**.

---

# What is Hashing?

Hashing is the process of converting data into a fixed-length string using a special mathematical function called a **hash function**.

For example,

```
Password:
MySecret@123
```

might become

```
$2b$12$4JlDkR9JcQjvX...
```

This new value is called a **hash**.

The important thing is that the original password cannot simply be read from this hash.

Instead of storing:

```
Username: Sujith
Password: MySecret@123
```

the database stores something like:

```
Username: Sujith
Password: $2b$12$4JlDkR9JcQjvX...
```

Even if someone steals the database, they won't immediately know your actual password.

---

# Why Can't We Just Encrypt Passwords?

A common question is:

> **Why don't websites encrypt passwords instead of hashing them?**

The difference is simple.

### Encryption

Encryption is designed so that the original data **can be recovered** using a secret key.

```
Password
    │
Encrypt
    ▼
Encrypted Password
    │
Decrypt
    ▼
Original Password
```

Encryption is useful when the original information needs to be read again, such as messages, documents, or payment details.

---

### Hashing

Hashing is different.

```
Password
    │
Hash Function
    ▼
Hash Value
```

There is **no reverse process** that converts the hash back into the original password.

The backend never needs to know your original password after you create your account.

It only needs a way to verify whether the password entered during login matches the one you originally chose.

---

# How Login Actually Works

When you register:

```
Password
      │
      ▼
Hash Function
      │
      ▼
Hash stored in Database
```

Later, during login:

```
User enters password
         │
         ▼
Hash Function
         │
         ▼
Generated Hash
         │
Compare
         │
Stored Hash in Database
```

If both hashes are identical, the password is correct.

Notice that the backend never compares plain-text passwords.

It compares **hashes**.

---

# What Makes Hashing Secure?

A good password hashing algorithm has several important properties.

### Same Input → Same Output

The same password always generates the same hash.

```
Hello123
↓

A8XK2...
```

Typing **Hello123** again will always produce the same hash.

---

### Small Change → Completely Different Hash

Changing even a single character produces an entirely different hash.

```
Hello123
↓

A8XK2...
```

```
Hello124
↓

P7Lm9...
```

This makes it extremely difficult to guess passwords by comparing similar hashes.

---

### One-Way Function

Hashing is designed to be one-way.

Given the hash,

```
$2b$12$4JlDkR9JcQjvX...
```

there is no practical way to recover

```
MySecret@123
```

This one-way property is what makes hashing suitable for storing passwords.

---

# What is Salt?

Suppose two users choose the exact same password.

```
Password123
```

Without additional protection, both users would produce the exact same hash.

Attackers could easily identify users who share passwords.

To prevent this, modern hashing algorithms add a random value called a **salt** before hashing.

```
Password
     +
Random Salt
        │
        ▼
Hash Function
        │
        ▼
Unique Hash
```

Even if two users choose the same password, their stored hashes will be completely different because each user has a different salt.

---

# Common Password Hashing Algorithms

Over time, several hashing algorithms have been developed.

Some are no longer considered secure for password storage.

|Algorithm|Suitable for Passwords?|Notes|
|---|---|---|
|MD5|❌ No|Too fast and easily cracked|
|SHA-1|❌ No|No longer considered secure|
|SHA-256|⚠️ Not recommended alone|Cryptographically strong but too fast for password storage|
|bcrypt|✅ Yes|Widely used in modern web applications|
|Argon2|✅ Yes|Modern and highly recommended|
|scrypt|✅ Yes|Designed to resist hardware attacks|

For most beginner and intermediate web applications, **bcrypt** is the most commonly used algorithm and is supported by many backend frameworks.

---

# The Big Picture

Authentication depends on secure password storage.

Instead of saving passwords directly:

```
User Password
        │
        ▼
Hash Function
        │
        ▼
Database
```

During login:

```
Entered Password
        │
        ▼
Hash Function
        │
        ▼
Compare with Stored Hash
        │
        ▼
Authentication Success or Failure
```

This simple process protects millions of user accounts every day.

---

# What's Next?

Now that the server can securely verify a user's identity, another question arises:

> **Once I log in successfully, how does the website remember that I'm already logged in while navigating between pages?**

We'll answer that in the next topic:

➡️ [[Sessions and Cookies]]
