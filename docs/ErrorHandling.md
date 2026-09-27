# ⚠️ Error Handling

## 🔹 What is Error Handling?

**Error handling** means detecting and properly handling errors that occur while running a Node.js application.

Instead of crashing the application or sending unclear responses, we can send a proper error message.

Example:

```text
Client Request
      ↓
Express Route
      ↓
Error occurs
      ↓
Error Handler
      ↓
Error Response
```

---

## 🔹 Basic try-catch

For synchronous code:

```js
app.get("/", (req, res) => {

    try {

        const result = 10 / 0;

        res.json({
            result: result
        });

    } catch (error) {

        res.status(500).json({
            message: "Something went wrong"
        });

    }

});
```

---

## 🔹 Express Error-Handling Middleware

Express provides special middleware for handling errors.

It has **4 parameters**:

```js
(err, req, res, next)
```

Example:

```js
app.use((err, req, res, next) => {

    res.status(500).json({
        message: "Internal Server Error"
    });

});
```

The `err` parameter identifies it as error-handling middleware.

---

## 🔹 Using `next(error)`

We can pass an error to the error-handling middleware using:

```js
next(error);
```

Example:

```js
app.get("/users", (req, res, next) => {

    try {

        throw new Error("Database error");

    } catch (error) {

        next(error);

    }

});
```

Error middleware:

```js
app.use((err, req, res, next) => {

    res.status(500).json({
        message: err.message
    });

});
```

Response:

```json
{
    "message": "Database error"
}
```

---

## 🔹 Custom Error Response

We can send different status codes.

```js
app.get("/user/:id", (req, res, next) => {

    const user = null;

    if (!user) {
        const error = new Error("User not found");
        error.status = 404;

        return next(error);
    }

    res.json(user);
});
```

Error handler:

```js
app.use((err, req, res, next) => {

    res.status(err.status || 500).json({
        message: err.message || "Server Error"
    });

});
```

---

## 🔹 404 Route Handling

A route that does not exist should return `404`.

```js
app.use((req, res) => {

    res.status(404).json({
        message: "Route not found"
    });

});
```

This is usually placed **after all valid routes**.

---

## 🔹 Error Middleware Order

A common Express structure is:

```js
const express = require("express");

const app = express();

app.use(express.json());

// Routes
app.get("/", (req, res) => {
    res.send("Home");
});

// 404 handler
app.use((req, res) => {
    res.status(404).json({
        message: "Route not found"
    });
});

// Error handler
app.use((err, req, res, next) => {
    res.status(err.status || 500).json({
        message: err.message || "Internal Server Error"
    });
});

app.listen(3000);
```

---

## 🔹 Common HTTP Error Codes

```text
400 → Bad Request
401 → Unauthorized
403 → Forbidden
404 → Not Found
409 → Conflict
500 → Internal Server Error
```

Example:

```js
res.status(400).json({
    message: "Invalid input"
});
```

---

## 🔹 Async Errors

When using asynchronous code, errors should also reach the error middleware.

Example:

```js
app.get("/users", async (req, res, next) => {

    try {

        const users = await getUsers();

        res.json(users);

    } catch (error) {

        next(error);

    }

});
```

This keeps error handling centralized.

---

## 🔹 Why Centralized Error Handling?

Instead of writing error responses repeatedly in every route, we can use one error-handling middleware.

```text
Route 1 ──┐
Route 2 ──┤
Route 3 ──┼──→ Error Middleware
Route 4 ──┘
```

Benefits:

- Consistent error responses
- Less duplicate code
- Easier debugging
- Cleaner routes

---

## 🎯 Interview Questions

### ❓ What is error handling?

> Error handling is the process of detecting and managing errors so the application can respond properly.

### ❓ How does Express identify error-handling middleware?

> Express identifies it by its four parameters: `(err, req, res, next)`.

### ❓ What is `next(error)`?

> `next(error)` passes an error to Express's error-handling middleware.

### ❓ What is a 404 error?

> A 404 status means the requested resource or route was not found.

### ❓ What is a 500 error?

> A 500 status means an unexpected error occurred on the server.

---

## 🧠 Quick Revision

```text
try-catch
   ↓
Catch Error
   ↓
next(error)
   ↓
Error Middleware
   ↓
Proper Response
```

Remember:

```js
(err, req, res, next)
```

is the standard Express error-handler signature.

### ⭐ Interview One-Liner

> **Express error handling uses try-catch and centralized error-handling middleware to catch errors and send appropriate HTTP responses to the client.**
