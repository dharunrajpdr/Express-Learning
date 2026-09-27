# 🛠️ CRUD API

## 🔹 What is CRUD?

**CRUD** represents the four basic operations performed on data:

```text
C → Create
R → Read
U → Update
D → Delete
```

In a REST API, CRUD operations are commonly implemented using HTTP methods.

---

## 🔹 CRUD and HTTP Methods

| CRUD Operation | HTTP Method | Example |
|---|---|---|
| Create | POST | `/users` |
| Read | GET | `/users` |
| Update | PUT / PATCH | `/users/101` |
| Delete | DELETE | `/users/101` |

---

## 🔹 Create

Used to create a new user.

```js
app.post("/users", (req, res) => {

    const user = req.body;

    res.status(201).json({
        message: "User created",
        user: user
    });

});
```

Request body:

```json
{
    "name": "Dharun",
    "age": 21
}
```

---

## 🔹 Read

Used to retrieve users.

```js
app.get("/users", (req, res) => {

    res.json({
        message: "Users fetched"
    });

});
```

To get one user:

```js
app.get("/users/:id", (req, res) => {

    res.json({
        id: req.params.id
    });

});
```

---

## 🔹 Update

Used to update an existing user.

```js
app.put("/users/:id", (req, res) => {

    const id = req.params.id;
    const user = req.body;

    res.json({
        message: "User updated",
        id: id,
        user: user
    });

});
```

---

## 🔹 Delete

Used to delete a user.

```js
app.delete("/users/:id", (req, res) => {

    const id = req.params.id;

    res.json({
        message: "User deleted",
        id: id
    });

});
```

---

## 🔹 Complete CRUD API

```js
const express = require("express");

const app = express();

app.use(express.json());

// CREATE
app.post("/users", (req, res) => {

    res.status(201).json({
        message: "User created",
        user: req.body
    });

});

// READ
app.get("/users", (req, res) => {

    res.json({
        message: "All users"
    });

});

// READ ONE
app.get("/users/:id", (req, res) => {

    res.json({
        message: "Single user",
        id: req.params.id
    });

});

// UPDATE
app.put("/users/:id", (req, res) => {

    res.json({
        message: "User updated",
        id: req.params.id,
        user: req.body
    });

});

// DELETE
app.delete("/users/:id", (req, res) => {

    res.json({
        message: "User deleted",
        id: req.params.id
    });

});

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

---

## 🔹 Real-World CRUD Flow

For a user management system:

```text
Create User
POST /users
      ↓
Database

Get Users
GET /users
      ↓
Database

Update User
PUT /users/101
      ↓
Database

Delete User
DELETE /users/101
      ↓
Database
```

---

## 🎯 Interview Questions

### ❓ What is CRUD?

> CRUD stands for Create, Read, Update, and Delete, which are the basic operations used to manage data.

### ❓ Which HTTP method is used for Create?

> POST.

### ❓ Which HTTP method is used for Read?

> GET.

### ❓ Which methods can be used for Update?

> PUT or PATCH.

### ❓ Which method is used for Delete?

> DELETE.

### ❓ What is a CRUD API?

> A CRUD API provides endpoints to create, read, update, and delete resources.

---

## 🧠 Quick Revision

```text
CREATE → POST
READ   → GET
UPDATE → PUT / PATCH
DELETE → DELETE
```

Example:

```text
POST   /users
GET    /users
GET    /users/101
PUT    /users/101
DELETE /users/101
```

### ⭐ Interview One-Liner

> **A CRUD API provides endpoints for creating, reading, updating, and deleting resources using HTTP methods such as POST, GET, PUT/PATCH, and DELETE.**
