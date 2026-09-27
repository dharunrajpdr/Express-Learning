# 🔗 Middleware

## 🔹 What is Middleware?

**Middleware** is a function that runs **between the client request and the final response**.

It can:

- Check authentication
- Log requests
- Modify request/response
- Validate data
- Handle errors

Simple flow:

```text
Client
   ↓
Request
   ↓
Middleware
   ↓
Route Handler
   ↓
Response
```

---

## 🔹 Basic Middleware

```js
const express = require("express");

const app = express();

app.use((req, res, next) => {
    console.log("Middleware executed");
    next();
});

app.get("/", (req, res) => {
    res.send("Home Page");
});

app.listen(3000);
```

Output in terminal:

```text
Middleware executed
```

---

## 🔹 What is `next()`?

`next()` passes control to the **next middleware or route handler**.

```js
app.use((req, res, next) => {
    console.log("First Middleware");

    next();
});
```

If we don't call `next()` and don't send a response, the request can remain waiting.

---

## 🔹 Multiple Middleware

```js
app.use((req, res, next) => {
    console.log("Middleware 1");
    next();
});

app.use((req, res, next) => {
    console.log("Middleware 2");
    next();
});

app.get("/", (req, res) => {
    res.send("Home");
});
```

Output:

```text
Middleware 1
Middleware 2
```

---

## 🔹 Logger Middleware

Middleware can log request information.

```js
app.use((req, res, next) => {

    console.log(req.method, req.url);

    next();
});
```

For:

```text
GET /users
```

Output:

```text
GET /users
```

---

## 🔹 Built-in Middleware

Express provides some built-in middleware.

### `express.json()`

Used to parse JSON request bodies.

```js
app.use(express.json());
```

Example request:

```json
{
    "name": "Dharun",
    "age": 21
}
```

Then:

```js
req.body
```

can access the parsed data.

---

## 🔹 Route-Specific Middleware

Middleware can be applied to a particular route.

```js
const checkAuth = (req, res, next) => {

    console.log("Checking authentication");

    next();
};

app.get("/profile", checkAuth, (req, res) => {
    res.send("Profile Page");
});
```

The middleware runs before the route handler.

---

## 🔹 Authentication Middleware

A simple example:

```js
const checkAuth = (req, res, next) => {

    const isLoggedIn = true;

    if (!isLoggedIn) {
        return res.status(401).send("Unauthorized");
    }

    next();
};

app.get("/dashboard", checkAuth, (req, res) => {
    res.send("Dashboard");
});
```

Flow:

```text
Request
   ↓
checkAuth
   ↓
Authenticated?
   ↓
next()
   ↓
Dashboard
```

---

## 🔹 Types of Middleware

| Type | Example |
|---|---|
| Application-level | `app.use()` |
| Route-level | Middleware for specific route |
| Built-in | `express.json()` |
| Third-party | `cors()`, `morgan()` |
| Error-handling | `(err, req, res, next)` |

---

## 🎯 Interview Questions

### ❓ What is middleware?

> Middleware is a function that executes during the request-response cycle and can process the request before passing control to the next middleware or route handler.

### ❓ What is `next()`?

> `next()` passes control to the next middleware or handler in the request-response cycle.

### ❓ Why is `express.json()` used?

> `express.json()` parses incoming JSON request bodies and makes the data available through `req.body`.

### ❓ Where is middleware used?

> Middleware is commonly used for authentication, logging, validation, parsing request data, CORS, and error handling.

---

## 🧠 Quick Revision

```text
Request
   ↓
Middleware
   ↓
next()
   ↓
Route Handler
   ↓
Response
```

Remember:

```text
Middleware → Process request
next()     → Continue
res.send() → End response
```

### ⭐ Interview One-Liner

> **Middleware is a function in Express.js that runs during the request-response cycle to process requests, perform checks, or modify data before passing control to the next handler.**
