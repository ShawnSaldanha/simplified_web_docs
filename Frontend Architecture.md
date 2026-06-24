# Frontend Architecture: Building What People See

Welcome to the frontend side of the house! If the backend is the hidden engine of a car, the frontend is the dashboard, the steering wheel, and the shiny paint job. It is everything a user sees, clicks, taps, and interacts with on their screen.

---

##  The Holy Trinity of the Web

Every single website or web app you have ever used is built on top of three core technologies. Think of them like building a house:

### 1. HTML (The Skeleton)
* **What it stands for:** HyperText Markup Language
* **What it does:** It defines the raw structure of the page. It tells the browser, "This is a heading, this is a paragraph, this is an image, and this is a button." 
* Without anything else, an HTML-only website looks like a plain Microsoft Word document from 1990's.
* *Find more about HTML [here](https://developer.mozilla.org/en-US/docs/Web/HTML)*

### 2. CSS (The Interior Design)
* **What it stands for:** Cascading Style Sheets
* **What it does:** It makes things look pretty. CSS controls the layout, colors, fonts, spacing, and sizing. It's how we say, "Make this button round, color it blue, and put it in the center of the screen."
* *Find more about CSS [here](https://developer.mozilla.org/en-US/docs/Web/CSS)*

### 3. JavaScript (The Electricity & Plumbing)
* **What it does:** It adds life and interactivity to the page. 
* Whenever you click a button and a pop-up window opens without reloading the page, or a feed automatically updates with new posts as you scroll—that is JavaScript hard at work.
* *Find more about JavaScript [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript)*

---

## Scaling Up: Modern Frontend Frameworks

As apps get bigger, writing raw HTML, CSS, and JavaScript gets messy *very* fast. Imagine trying to update a navigation bar across 500 different website pages manually. It's a nightmare.

To solve this, developers use **Frameworks** and **Libraries**. You've probably heard names like **React, Next , or Angular**. 

Instead of building pages from scratch every time, these tools let us build with **Components**:
* Think of components like **Lego bricks**. 
* You build a single `ProductCard` component or a `Navbar` component once, and then you can reuse it hundreds of times across your entire app. 
* If you need to change how the button looks, you change it in *one* place, and it updates everywhere instantly.
References
[React](https://react.dev/learn)
[Next.js](https://nextjs.org/learn/dashboard-app)
[Angular](https://angular.dev/tutorials/learn-angular)

Moreover , usually we don not build components from scratch always instead we use the approach of using readymade components and then tweaking them if theres a need , i'll be attaching a few of the famous UI component libraries for Next.js for better understanding and reference
[MaterialUI](https://mui.com/material-ui/all-components/)
[ShadCN](https://ui.shadcn.com/docs/components)
**NOTE** : *These are just for reference there are many more such libraries with really good components*

---

## What is State Management?

When people start learning frontend, "State" is a word that confuses a lot of folks, but it's actually super simple. 

>  **The Simple Definition:** State is just the *current memory* of the app. It's a snapshot of whatever data is happening right now.

**For example, on a shopping website:**
* Is the user logged in? *(Yes/No)* $\rightarrow$ That's state.
* What items are currently in their shopping cart? $\rightarrow$ That's state.
* Did they click the dark mode toggle switch? *(True/False)* $\rightarrow$ That's state.

Frontend code is constantly watching the "state," and whenever the state changes (like adding an item to a cart), the screen instantly updates to show the new number.

---

## 🔗 How Frontend Talks to Backend

The frontend doesn't usually store data permanently. If you refresh the page and your cart is still there, it's because the frontend fetched that data from the backend.

The frontend talks to the backend using something called an **API (Application Programming Interface)**. 
* It sends an HTTP Request (like we talked about on the Home Page).
* The backend sends back a text format called **JSON** (which just looks like a neat list of keys and values).
* The frontend takes that raw JSON data and plugs it into the HTML/CSS components to make it look beautiful.

---

##  Where to Go From Here?

* To understand how the backend processes those requests and sends back that JSON data, head over to **[[Backend Systems]]**.
* To see how we protect that data while it travels through the air, check out **[[Security Foundations]]**.