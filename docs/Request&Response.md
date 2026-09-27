# 📩 Request & Response

## 🔹 What are Request and Response?

In Express.js:

- **Request (`req`)** → Information sent by the client to the server.
- **Response (`res`)** → Information sent by the server back to the client.

Simple flow:

```text
Client
   ↓
Request (req)
   ↓
Express Server
   ↓
Response (res)
   ↓
Client
```

---

## 🔹 Request Object (`req`)

The `req` object contains information about the incoming request.

Common properties:

```js
req.method
req.url
req.params
req.query
req.body
req.headers
```

Example:

```js
app.get("/users", (req, res) => {

    console.log(req.method);
    console.log(req.url);

    res.send("Users");
});
```

Output:

```text
GET
/users
```

---

## 🔹 Response Object (`res`)

The `res` object is used to send a response to the client.

Common methods:

```js
res.send()
res.json()
res.status()
res.end()
```

---

## 🔹 `res.send()`

Sends a response to the client.

```js
app.get("/", (req, res) => {
    res.send("Hello Express");
});
```

Output:

```text
Hello Express
```

---

## 🔹 `res.json()`

Used to send JSON data.

```js
app.get("/user", (req, res) => {

    res.json({
        name: "Dharun",
        age: 21
    });

});
```

Response:

```json
{
    "name": "Dharun",
    "age": 21
}
```

---

## 🔹 `res.status()`

Sets the HTTP status code.

```js
app.get("/user", (req, res) => {

    res.status(200).json({
        message: "User found"
    });

});
```

Example error:

```js
res.status(404).json({
    message: "User not found"
});
```

---

## 🔹 Request Headers

Headers contain additional information about the request.

```js
app.get("/", (req, res) => {

    console.log(req.headers);

    res.send("Hello");
});
```

A specific header:

```js
const token = req.headers.authorization;
```

---

## 🔹 Complete Example

```js
const express = require("express");

const app = express();

app.get("/user", (req, res) => {

    console.log("Method:", req.method);
    console.log("URL:", req.url);

    res.status(200).json({
        name: "Dharun",
        role: "Developer"
    });
});

app.listen(3000);
```

Request:

```text
GET /user
```

Response:

```json
{
    "name": "Dharun",
    "role": "Developer"
}
```

---

## 🔹 Request vs Response

| Request (`req`) | Response (`res`) |
|---|---|
| Comes from client | Sent by server |
| Contains request information | Contains response information |
| `req.body` | `res.json()` |
| `req.params` | `res.status()` |
| `req.query` | `res.send()` |
| `req.headers` | `res.end()` |

---

## 🎯 Interview Questions

### ❓ What is `req`?

> `req` is the Express request object that contains information about the incoming client request.

### ❓ What is `res`?

> `res` is the Express response object used to send data and status codes back to the client.

### ❓ What is the difference between `res.send()` and `res.json()`?

> `res.send()` can send different types of responses, while `res.json()` is specifically used to send JSON data.

### ❓ How do you set a status code?

```js
res.status(404).json({
    message: "Not Found"
});
```

---

## 🧠 Quick Revision

```text
req → Client → Server
res → Server → Client
```

```text
req.method   → HTTP method
req.url      → URL
req.params   → Route parameters
req.query    → Query parameters
req.body     → Request body
req.headers  → Request headers
```

```text
res.send()   → Send response
res.json()   → Send JSON
res.status() → Set status code
```

### ⭐ Interview One-Liner

> **In Express.js, `req` contains information about the client request, while `res` is used by the server to send the response back to the client.**
