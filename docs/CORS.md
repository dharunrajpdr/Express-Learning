# 🌍 CORS

## 🔹 What is CORS?

**CORS** stands for **Cross-Origin Resource Sharing**.

It controls whether a browser allows a frontend from one **origin** to access resources from another origin.

Example:

```text
React Frontend
http://localhost:5173
        ↓
        API Request
        ↓
Express Backend
http://localhost:3000
```

These are different origins because their ports are different.

---

## 🔹 Why is CORS Needed?

Browsers apply security rules to cross-origin requests.

For example:

```text
Frontend → localhost:5173
Backend  → localhost:3000
```

The backend needs to allow the frontend origin if the browser is going to permit the response to be accessed.

---

## 🔹 Installing CORS

Install the `cors` package:

```bash
npm install cors
```

---

## 🔹 Basic CORS Setup

```js
const express = require("express");
const cors = require("cors");

const app = express();

app.use(cors());

app.get("/", (req, res) => {
    res.json({
        message: "Hello from server"
    });
});

app.listen(3000);
```

This allows cross-origin requests according to the CORS middleware configuration.

---

## 🔹 Allow a Specific Origin

Instead of allowing every origin, we can specify one.

```js
app.use(cors({
    origin: "http://localhost:5173"
}));
```

Now the server allows requests from:

```text
http://localhost:5173
```

---

## 🔹 Multiple Origins

We can configure multiple allowed origins.

```js
const allowedOrigins = [
    "http://localhost:5173",
    "https://example.com"
];

app.use(cors({
    origin: allowedOrigins
}));
```

In real applications, origin validation may be configured with a function when the allowed list is dynamic.

---

## 🔹 CORS with Credentials

If authentication uses cookies, credentials may need to be enabled.

Backend:

```js
app.use(cors({
    origin: "http://localhost:5173",
    credentials: true
}));
```

Frontend with Axios:

```js
axios.get("http://localhost:3000/user", {
    withCredentials: true
});
```

The server must be configured to allow the specific frontend origin when credentials are used.

---

## 🔹 Common CORS Error

You may see an error similar to:

```text
Access to XMLHttpRequest has been blocked by CORS policy
```

This usually means the browser did not allow the cross-origin response because the server's CORS configuration does not permit that request.

---

## 🔹 CORS vs Same-Origin Policy

### Same-Origin Policy

A browser security mechanism that restricts how a web page can interact with resources from another origin.

### CORS

A mechanism that allows a server to specify which cross-origin requests browsers may allow.

Simple memory:

```text
Same-Origin Policy → Browser Security Rule

CORS → Server-controlled permission for cross-origin access
```

---

## 🔹 What is an Origin?

An origin is made up of:

```text
Protocol + Host + Port
```

Example:

```text
http://localhost:5173
```

Here:

```text
Protocol → http
Host     → localhost
Port     → 5173
```

These are different origins:

```text
http://localhost:5173
http://localhost:3000
```

because the ports are different.

---

## 🎯 Interview Questions

### ❓ What is CORS?

> CORS is a browser security mechanism that allows a server to specify which cross-origin requests are permitted.

### ❓ Why do we use the `cors` package in Express?

> It provides middleware for configuring CORS rules for an Express application.

### ❓ What does `origin` mean in CORS?

> It specifies which origin is allowed to make cross-origin requests.

### ❓ What does `credentials: true` do?

> It allows the CORS configuration to support credentialed requests such as cookies, when the browser and server are configured accordingly.

---

## 🧠 Quick Revision

```text
Frontend
localhost:5173
      ↓
   CORS
      ↓
Backend
localhost:3000
```

Basic setup:

```js
const cors = require("cors");

app.use(cors());
```

Specific origin:

```js
app.use(cors({
    origin: "http://localhost:5173"
}));
```

With cookies:

```js
app.use(cors({
    origin: "http://localhost:5173",
    credentials: true
}));
```

### ⭐ Interview One-Liner

> **CORS allows a server to control which cross-origin requests a browser is permitted to access.**
