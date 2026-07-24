# Welcome to the Web Development Map

Hey! If you're looking to understand how the web actually works without drowning in a sea of intense computer science jargon, you're in the right place.

Instead of a massive, boring textbook, this guide is built like a web of connected notes. You can read through this home page to get the big picture, and then click on the internal links to dive into specific topics whenever you're ready.

---

## The Big Picture: The Internet in 30 Seconds

At its absolute core, the entire internet is just a massive, ongoing game of catch between two things: **The Client** and **The Server**.

Whenever you tap a button on an app or type a website name into your browser, a quick chain reaction happens behind the scenes:

### 1. The Request (The Client Side)

The **Client** is the device or application you're using right now—like your phone, laptop, or a web browser (Chrome, Edge, Safari, etc.).

- When you click a button or open a webpage, the client packages your action into a message called an **HTTP Request**.
    
- Think of it like ordering food at a restaurant. You're telling the kitchen, _"I'd like to see my profile page."_
    
- To learn how we build everything users can see and interact with, check out **[[Frontend Architecture]]**.
    

### 2. The Journey (Networking)

Once the request leaves your device, it has to travel across the internet to reach the correct server.

Along the way, several networking technologies work together behind the scenes:

- **DNS** translates website names into IP addresses.
    
- **Routers** decide where the request should travel.
    
- **TCP/IP** ensures data reaches the correct destination reliably.
    
- Various internet protocols help different devices communicate with one another.
    

Although this all happens in just a few milliseconds, it's one of the most important parts of how the web works.

To understand how requests actually travel across the internet, check out **[[Networking Concepts]]**.

### 3. The Processing (The Server & Database)

Your request eventually reaches a **Server**, which is simply a powerful computer running applications 24/7 inside a data center.

The server:

- Receives the request.
    
- Decides what needs to be done.
    
- Talks to a **Database** if it needs to retrieve or store information (such as your account details or saved posts).
    
- Prepares the response.
    

To learn how we build this backend logic using Java, Spring, Spring Boot, and databases, check out **[[Backend Systems and Server-Side Architecture]]**.

### 4. The Response

Once the server finishes processing your request, it packages the result into an **HTTP Response** and sends it back across the internet.

Along with the data, it also includes a **status code**, such as:

- **200 OK** – Everything worked successfully.
    
- **404 Not Found** – The requested page couldn't be found.
    
- **500 Internal Server Error** – Something went wrong on the server.
    

Your browser receives this response and immediately renders the webpage you see on your screen.

---

## Choose Your Path

Ready to dive deeper? Pick any topic below and explore it at your own pace.

- **[[Frontend Architecture]]** – Learn how websites are built using HTML, CSS, JavaScript, and modern frontend frameworks.
    
- **[[Backend Systems and Server-Side Architecture]]** – Discover how servers process requests, implement business logic, and communicate with databases.
    
- **[[Networking Concepts]]** – Understand how data travels across the internet, how devices communicate, and why technologies like DNS, IP addresses, routers, TCP, and HTTP are essential.
    
- **[[Microservices & Distributed Systems]]** – Explore how large applications are split into multiple independent services that work together.
    
- **[[Security Foundations]]** – Learn the fundamentals of authentication, authorization, HTTPS, JWTs, OAuth, and protecting user data.
    

---

## Note

If you'd like to learn more about HTML, CSS, JavaScript, browser APIs, and other web technologies, the **MDN Web Docs** is one of the best resources available:

[https://developer.mozilla.org/en-US/](https://developer.mozilla.org/en-US/)
