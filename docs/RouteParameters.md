# 🔢 Route Parameters

## 🔹 What are Route Parameters?

**Route parameters** are dynamic values included in the URL.

They are defined using `:`.

Example:

```js
app.get("/users/:id", (req, res) => {
    res.send(`User ID: ${req.params.id}`);
});
```

Request:

```text
GET /users/101
```

Output:

```text
User ID: 101
```

Here:

```js
req.params.id
```

is:

```text
101
```

---

## 🔹 Why Use Route Parameters?

They are useful when we want to identify a specific resource.

Examples:

```text
/users/101
/products/50
/orders/200
/posts/10
```

Here the ID changes dynamically.

---

## 🔹 Basic Syntax

```js
app.get("/users/:id", (req, res) => {
    console.log(req.params.id);
});
```

General syntax:

```text
/:parameterName
```

Access it using:

```js
req.params.parameterName
```

---

## 🔹 Multiple Parameters

We can have multiple route parameters.

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

## 🔹 Route Parameter vs Query Parameter

### Route Parameter

```text
/users/101
```

Code:

```js
req.params.id
```

### Query Parameter

```text
/users?id=101
```

Code:

```js
req.query.id
```

| Route Parameter | Query Parameter |
|---|---|
| `/users/101` | `/users?id=101` |
| `req.params.id` | `req.query.id` |
| Usually identifies a resource | Usually filters/options/search |
| Defined in route | Added after `?` |

---

## 🔹 Example with Product

```js
app.get("/products/:id", (req, res) => {

    const productId = req.params.id;

    res.json({
        message: "Product found",
        id: productId
    });

});
```

Request:

```text
/products/500
```

Response:

```json
{
    "message": "Product found",
    "id": "500"
}
```

---

## 🔹 Important Point

Route parameter values are received as **strings**.

Example:

```js
app.get("/users/:id", (req, res) => {

    console.log(typeof req.params.id);

    res.send("Done");
});
```

For:

```text
/users/101
```

Output:

```text
string
```

If you need a number:

```js
const id = Number(req.params.id);
```

---

## 🎯 Interview Questions

### ❓ What is a route parameter?

> A route parameter is a dynamic value defined inside an Express route URL using `:`.

### ❓ How do you access route parameters?

```js
req.params
```

Example:

```js
req.params.id
```

### ❓ What is the difference between `req.params` and `req.query`?

> `req.params` contains values defined in the route path, while `req.query` contains values provided after `?` in the URL.

---

## 🧠 Quick Revision

```text
Route:
 /users/:id

Request:
 /users/101

Access:
 req.params.id

Value:
 "101"
```

### ⭐ Interview One-Liner

> **Route parameters are dynamic values in an Express URL, defined using `:` and accessed through `req.params`.**
