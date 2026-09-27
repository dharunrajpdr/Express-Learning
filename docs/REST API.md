# 🔗 REST API

## 🔹 What is REST API?

**REST API** stands for **Representational State Transfer Application Programming Interface**.

It is a way for a **client and server to communicate using HTTP methods**.

Example:

```text
React Frontend
      ↓
   REST API
      ↓
Node.js + Express
      ↓
   Database
```

---

## 🔹 Common REST Methods

```text
GET     → Read
POST    → Create
PUT     → Update
PATCH   → Partial Update
DELETE  → Delete
```

---

## 🔹 Example REST API

For a `users` resource:

```text
GET    /users
POST   /users
GET    /users/101
PUT    /users/101
PATCH  /users/101
DELETE /users/101
```

Each URL represents a **resource**.

---

## 🔹 Express Example

```js
const express = require("express");

const app = express();

app.use(express.json());

app.get("/users", (req, res) => {
    res.json({
        message: "Get all users"
    });
});

app.post("/users", (req, res) => {
    res.status(201).json({
        message: "Create user"
    });
});

app.get("/users/:id", (req, res) => {
    res.json({
        message: "Get user",
        id: req.params.id
    });
});

app.put("/users/:id", (req, res) => {
    res.json({
        message: "Update user"
    });
});

app.delete("/users/:id", (req, res) => {
    res.json({
        message: "Delete user"
    });
});

app.listen(3000);
```

---

## 🔹 REST API Response

REST APIs commonly exchange data using **JSON**.

Example:

```json
{
    "id": 101,
    "name": "Dharun",
    "email": "dharun@example.com"
}
```

---

## 🔹 Important REST Principles

### 1. Resource-Based URLs

Use nouns instead of actions.

Good:

```text
GET /users
GET /products
```

Avoid:

```text
GET /getUsers
GET /getProducts
```

---

### 2. Use HTTP Methods

The HTTP method describes the action.

```text
GET    /users
POST   /users
DELETE /users/101
```

---

### 3. Stateless

Each request should contain the information needed to process it.

The server should not depend on previous requests being remembered as part of the REST interaction.

---

### 4. Use HTTP Status Codes

Common status codes:

```text
200 → Success
201 → Created
400 → Bad Request
401 → Unauthorized
403 → Forbidden
404 → Not Found
500 → Server Error
```

Example:

```js
res.status(404).json({
    message: "User not found"
});
```

---

## 🔹 REST API Example in MERN

```text
React
  ↓
Axios / Fetch
  ↓
Express REST API
  ↓
Node.js
  ↓
MongoDB
```

Example:

```text
React
  ↓
GET /api/users
  ↓
Express Route
  ↓
MongoDB
  ↓
JSON Response
  ↓
React
```

---

## 🔹 REST API vs API

**API** is a general term for an interface that allows software systems to communicate.

**REST API** is an API designed around REST principles and commonly uses HTTP.

```text
API
 └── REST API
```

---

## 🎯 Interview Questions

### ❓ What is a REST API?

> A REST API is an HTTP-based API that allows clients and servers to communicate using resources, HTTP methods, and standard status codes.

### ❓ What does REST stand for?

> Representational State Transfer.

### ❓ What format is commonly used in REST APIs?

> JSON is the most commonly used format.

### ❓ What does stateless mean in REST?

> Each request should contain the information required to process it, without depending on stored client session state on the server.

### ❓ Give an example of a REST API endpoint.

```text
GET /users/101
```

It can be used to retrieve user `101`.

---

## 🧠 Quick Revision

```text
REST API
   ↓
Resources + HTTP Methods + Status Codes
```

```text
GET    → Read
POST   → Create
PUT    → Update
PATCH  → Partial Update
DELETE → Delete
```

Example:

```text
GET /users
GET /users/101
POST /users
PUT /users/101
DELETE /users/101
```

### ⭐ Interview One-Liner

> **A REST API is an HTTP-based interface that allows clients and servers to communicate through resources, standard HTTP methods, and status codes.**
