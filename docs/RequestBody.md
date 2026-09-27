# 📦 Request Body

## 🔹 What is Request Body?

The **request body** contains data sent by the client to the server.

It is commonly used with:

```text
POST
PUT
PATCH
```

Example:

```json
{
    "name": "Dharun",
    "age": 21
}
```

---

## 🔹 Access Request Body

In Express, JSON request data can be accessed using:

```js
req.body
```

But first, we need:

```js
app.use(express.json());
```

---

## 🔹 Basic Example

```js
const express = require("express");

const app = express();

app.use(express.json());

app.post("/users", (req, res) => {

    console.log(req.body);

    res.json({
        message: "User received",
        user: req.body
    });
});

app.listen(3000);
```

Send:

```json
{
    "name": "Dharun",
    "age": 21
}
```

Response:

```json
{
    "message": "User received",
    "user": {
        "name": "Dharun",
        "age": 21
    }
}
```

---

## 🔹 Why `express.json()`?

Express needs JSON body parsing middleware to read incoming JSON requests.

```js
app.use(express.json());
```

Without it, `req.body` may be `undefined` for JSON requests.

---

## 🔹 Request Body vs Query Parameters

### Request Body

```text
POST /users
```

Body:

```json
{
    "name": "Dharun",
    "age": 21
}
```

Access:

```js
req.body
```

### Query Parameters

```text
GET /users?name=Dharun
```

Access:

```js
req.query.name
```

---

## 🔹 Request Body vs Route Parameters

### Route Parameter

```text
/users/101
```

```js
req.params.id
```

### Request Body

```json
{
    "name": "Dharun"
}
```

```js
req.body.name
```

---

## 🔹 Example: Create User

```js
app.post("/users", (req, res) => {

    const { name, email } = req.body;

    res.status(201).json({
        message: "User created",
        name: name,
        email: email
    });
});
```

Request body:

```json
{
    "name": "Dharun",
    "email": "dharun@example.com"
}
```

Response:

```json
{
    "message": "User created",
    "name": "Dharun",
    "email": "dharun@example.com"
}
```

---

## 🔹 Content-Type

For JSON request data, the client should send:

```text
Content-Type: application/json
```

Example:

```text
POST /users
Content-Type: application/json
```

Body:

```json
{
    "name": "Dharun"
}
```

---

## 🔹 Common Body Types

Express applications may receive different types of request bodies.

```text
JSON
Form URL Encoded
Multipart/Form Data
```

For JSON:

```js
app.use(express.json());
```

For URL-encoded form data:

```js
app.use(express.urlencoded({ extended: true }));
```

File uploads commonly use middleware such as `multer`.

---

## 🎯 Interview Questions

### ❓ What is `req.body`?

> `req.body` contains data sent by the client in the request body.

### ❓ Why do we use `express.json()`?

> It parses incoming JSON request bodies and makes the parsed data available through `req.body`.

### ❓ When is request body commonly used?

> It is commonly used with POST, PUT, and PATCH requests to send data to the server.

### ❓ What is Content-Type?

> `Content-Type` tells the server what type of data is being sent in the request body.

---

## 🧠 Quick Revision

```text
Client
   ↓
POST /users
   ↓
JSON Body
   ↓
express.json()
   ↓
req.body
   ↓
Route Handler
   ↓
Response
```

Remember:

```text
req.params → Route parameters
req.query  → Query parameters
req.body   → Request body
```

### ⭐ Interview One-Liner

> **The request body contains data sent by the client to the server, and in Express JSON data can be accessed using `req.body` after enabling `express.json()`.**
