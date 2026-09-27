# 🛣️ Routing

## 🔹 What is Routing?

**Routing** means defining how an Express server responds to requests for different **URLs and HTTP methods**.

Example:

```text
GET /        → Home
GET /about   → About
GET /users   → Users
```

---

## 🔹 Basic Route

```js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Home Page");
});

app.listen(3000);
```

Open:

```text
http://localhost:3000/
```

Output:

```text
Home Page
```

---

## 🔹 Different Routes

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

```text
/         → Home
/about    → About
/contact  → Contact
```

---

## 🔹 HTTP Methods in Routing

Express supports different HTTP methods.

```js
app.get("/users", (req, res) => {
    res.send("Get Users");
});

app.post("/users", (req, res) => {
    res.send("Create User");
});

app.put("/users/:id", (req, res) => {
    res.send("Update User");
});

app.delete("/users/:id", (req, res) => {
    res.send("Delete User");
});
```

Common methods:

```text
GET     → Read
POST    → Create
PUT     → Update
PATCH   → Partial Update
DELETE  → Delete
```

---

## 🔹 Route Parameters

Parameters are dynamic values inside the URL.

```js
app.get("/users/:id", (req, res) => {
    res.send(`User ID: ${req.params.id}`);
});
```

Request:

```text
/users/101
```

Output:

```text
User ID: 101
```

Here:

```js
req.params.id
```

contains:

```text
101
```

---

## 🔹 Multiple Route Parameters

```js
app.get("/users/:userId/posts/:postId", (req, res) => {

    res.json({
        userId: req.params.userId,
        postId: req.params.postId
    });

});
```

Request:

```text
/users/10/posts/50
```

Response:

```json
{
    "userId": "10",
    "postId": "50"
}
```

---

## 🔹 Route Not Found

We can handle unknown routes:

```js
app.use((req, res) => {
    res.status(404).send("Route Not Found");
});
```

Example:

```text
GET /unknown
```

Response:

```text
Route Not Found
```

---

## 🔹 Route Order

Express checks routes in the order they are defined.

```js
app.get("/users", (req, res) => {
    res.send("Users");
});

app.get("*", (req, res) => {
    res.send("Not Found");
});
```

The general fallback route should come after the specific routes.

---

## 🔹 Routing Flow

```text
Client Request
      ↓
HTTP Method + URL
      ↓
Express Router
      ↓
Matching Route
      ↓
Route Handler
      ↓
Response
```

---

## 🎯 Interview Questions

### ❓ What is routing?

> Routing is the process of defining how an application responds to different URLs and HTTP methods.

### ❓ How do you create a GET route?

```js
app.get("/users", (req, res) => {
    res.send("Users");
});
```

### ❓ What is a route parameter?

> A route parameter is a dynamic value included in the URL, accessed using `req.params`.

### ❓ How do you handle a route that does not exist?

> We can add a fallback handler that returns a `404` response.

---

## 🧠 Quick Revision

```text
Routing
   ↓
URL + HTTP Method
   ↓
Matching Route
   ↓
Handler
   ↓
Response
```

```text
app.get()
app.post()
app.put()
app.patch()
app.delete()
```

### ⭐ Interview One-Liner

> **Routing in Express.js defines how the server handles requests for different URLs and HTTP methods.**
