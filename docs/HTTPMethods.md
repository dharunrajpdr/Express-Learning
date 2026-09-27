# 🌐 HTTP Methods

## 🔹 What are HTTP Methods?

**HTTP methods** define what action the client wants the server to perform.

The most commonly used methods are:

```text
GET
POST
PUT
PATCH
DELETE
```

---

## 🔹 GET

Used to **retrieve data** from the server.

Example:

```js
app.get("/users", (req, res) => {
    res.json({
        message: "Get users"
    });
});
```

Request:

```text
GET /users
```

---

## 🔹 POST

Used to **create new data**.

```js
app.post("/users", (req, res) => {
    res.status(201).json({
        message: "User created"
    });
});
```

Request:

```text
POST /users
```

Usually data is sent through:

```js
req.body
```

---

## 🔹 PUT

Used to **replace/update an existing resource**.

```js
app.put("/users/:id", (req, res) => {
    res.json({
        message: "User updated"
    });
});
```

Request:

```text
PUT /users/101
```

---

## 🔹 PATCH

Used to **partially update an existing resource**.

```js
app.patch("/users/:id", (req, res) => {
    res.json({
        message: "User partially updated"
    });
});
```

Example:

```json
{
    "name": "Dharun"
}
```

Only the name may be updated.

---

## 🔹 DELETE

Used to **delete a resource**.

```js
app.delete("/users/:id", (req, res) => {
    res.json({
        message: "User deleted"
    });
});
```

Request:

```text
DELETE /users/101
```

---

## 🔹 CRUD and HTTP Methods

HTTP methods are commonly mapped to CRUD operations:

| CRUD | HTTP Method | Purpose |
|---|---|---|
| Create | POST | Create data |
| Read | GET | Retrieve data |
| Update | PUT/PATCH | Update data |
| Delete | DELETE | Delete data |

Easy memory:

```text
POST   → Create
GET    → Read
PUT    → Update
PATCH  → Partial Update
DELETE → Delete
```

---

## 🔹 Complete Example

```js
const express = require("express");

const app = express();

app.use(express.json());

// Create
app.post("/users", (req, res) => {
    res.status(201).json({
        message: "User created"
    });
});

// Read
app.get("/users", (req, res) => {
    res.json({
        message: "Users fetched"
    });
});

// Update
app.put("/users/:id", (req, res) => {
    res.json({
        message: "User updated"
    });
});

// Partial Update
app.patch("/users/:id", (req, res) => {
    res.json({
        message: "User partially updated"
    });
});

// Delete
app.delete("/users/:id", (req, res) => {
    res.json({
        message: "User deleted"
    });
});

app.listen(3000);
```

---

## 🔹 PUT vs PATCH

### PUT

Usually represents replacing the resource with a new complete representation.

```text
PUT /users/101
```

```json
{
    "name": "Dharun",
    "email": "dharun@example.com",
    "age": 21
}
```

### PATCH

Usually represents changing only specific fields.

```text
PATCH /users/101
```

```json
{
    "age": 22
}
```

Simple memory:

```text
PUT   → Full Update
PATCH → Partial Update
```

---

## 🎯 Interview Questions

### ❓ What is GET?

> GET is used to retrieve data from the server.

### ❓ What is POST?

> POST is used to create a new resource.

### ❓ What is the difference between PUT and PATCH?

> PUT generally replaces the resource, while PATCH is used for partial updates.

### ❓ What is DELETE?

> DELETE is used to remove a resource from the server.

### ❓ Which HTTP method is commonly used to create data?

> POST.

---

## 🧠 Quick Revision

```text
GET     → Read
POST    → Create
PUT     → Full Update
PATCH   → Partial Update
DELETE  → Delete
```

### ⭐ Interview One-Liner

> **HTTP methods specify the operation a client wants to perform on a server resource, such as GET for reading, POST for creating, PUT/PATCH for updating, and DELETE for removing data.**
