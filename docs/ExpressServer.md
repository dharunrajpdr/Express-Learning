# 🚀 Express Server

## 🔹 What is an Express Server?

An **Express server** is a Node.js server created using the Express.js framework.

It listens for client requests and sends responses.

```text
Client
   ↓
Express Server
   ↓
Request Handling
   ↓
Response
```

---

## 🔹 Create an Express Server

First install Express:

```bash
npm install express
```

Create `app.js`:

```js
const express = require("express");

const app = express();

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

Run:

```bash
node app.js
```

Output:

```text
Server running on port 3000
```

---

## 🔹 Add a Route

```js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Hello Express Server");
});

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

Open:

```text
http://localhost:3000
```

Output:

```text
Hello Express Server
```

---

## 🔹 `app.listen()`

`app.listen()` starts the Express server on a specified port.

```js
app.listen(3000);
```

With a callback:

```js
app.listen(3000, () => {
    console.log("Server started");
});
```

---

## 🔹 Using Environment Variables

Instead of hardcoding the port:

```js
const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

If `PORT` is not provided, it uses:

```text
3000
```

---

## 🔹 Basic Express Server Structure

```text
express-app/
├── node_modules/
├── app.js
├── package.json
└── package-lock.json
```

`app.js`:

```js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Welcome");
});

app.listen(3000, () => {
    console.log("Server started");
});
```

---

## 🔹 Multiple Routes

```js
app.get("/", (req, res) => {
    res.send("Home");
});

app.get("/about", (req, res) => {
    res.send("About");
});

app.get("/contact", (req, res) => {
    res.send("Contact");
});
```

URLs:

```text
/        → Home
/about   → About
/contact → Contact
```

---

## 🔹 Express Request Flow

```text
Client
  ↓
Request
  ↓
Express Server
  ↓
Route
  ↓
Handler
  ↓
Response
  ↓
Client
```

---

## 🎯 Interview Questions

### ❓ How do you create an Express server?

> Create an Express application using `express()` and start it using `app.listen()`.

### ❓ What does `express()` do?

> It creates an Express application instance.

### ❓ What does `app.listen()` do?

> It starts the Express server and listens for incoming requests on a specified port.

### ❓ What is the default port of Express?

> Express does not have a fixed default port. We choose the port, commonly `3000` during development.

---

## 🧠 Quick Revision

```js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Hello");
});

app.listen(3000);
```

Remember:

```text
express()    → Create app
app.get()    → Create GET route
app.listen() → Start server
res.send()   → Send response
```

### ⭐ Interview One-Liner

> **An Express server is created using `express()` and started using `app.listen()` to handle incoming client requests.**
