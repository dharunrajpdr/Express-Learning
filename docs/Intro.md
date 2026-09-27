# 🚀 Express.js Introduction

## 🔹 What is Express.js?

**Express.js** is a lightweight and flexible **web framework for Node.js**.

It makes it easier to build:

- 🌐 Web servers
- 🔗 REST APIs
- 🛣️ Routes
- 🔐 Authentication
- 🛠️ Backend applications

Express.js is built on top of Node.js.

```text
JavaScript
    ↓
Node.js
    ↓
Express.js
    ↓
Backend / REST API
```

---

## 🔹 Why Use Express.js?

Creating a server directly with Node.js HTTP module can require more code.

### Node.js HTTP

```js
const http = require("http");

const server = http.createServer((req, res) => {
    if (req.url === "/") {
        res.end("Home");
    }
});

server.listen(3000);
```

### Express.js

```js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Home");
});

app.listen(3000);
```

Express provides simpler APIs for common backend tasks.

---

## 🔹 Install Express

Create a project:

```bash
mkdir express-app
cd express-app
npm init -y
```

Install Express:

```bash
npm install express
```

---

## 🔹 Basic Express Application

Create:

```text
app.js
```

Code:

```js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Hello Express");
});

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

Run:

```bash
node app.js
```

Open:

```text
http://localhost:3000
```

Output:

```text
Hello Express
```

---

## 🔹 Important Express Features

| Feature | Purpose |
|---|---|
| Routing | Handle different URLs |
| Middleware | Process requests |
| Request/Response | Handle client communication |
| REST APIs | Build backend APIs |
| Error Handling | Handle application errors |
| Authentication | Protect APIs |
| Static Files | Serve files |

---

## 🔹 Node.js vs Express.js

| Node.js | Express.js |
|---|---|
| JavaScript runtime | Web framework |
| Provides HTTP module | Built on Node.js |
| Lower-level APIs | Higher-level APIs |
| Can create servers | Makes server/API development easier |
| Runtime environment | Backend framework |

Simple memory:

```text
Node.js → Runtime
Express.js → Framework
```

---

## 🎯 Interview Questions

### ❓ What is Express.js?

> Express.js is a lightweight web framework for Node.js used to build web servers and REST APIs.

### ❓ Why do we use Express.js?

> Express.js simplifies server creation, routing, middleware handling, and API development in Node.js.

### ❓ Is Express.js a programming language?

> No. Express.js is a web framework built on top of Node.js.

### ❓ Is Express.js built on Node.js?

> Yes. Express.js runs on Node.js and provides a simpler way to build backend applications.

---

## 🧠 Quick Revision

```text
Node.js
   ↓
Express.js
   ↓
Routes + Middleware
   ↓
REST APIs
   ↓
Backend Application
```

### ⭐ Interview One-Liner

> **Express.js is a lightweight Node.js web framework used to build servers, REST APIs, routes, and backend applications efficiently.**
