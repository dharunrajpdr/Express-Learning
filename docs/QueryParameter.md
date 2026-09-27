# 🔍 Query Parameters

## 🔹 What are Query Parameters?

**Query parameters** are values added to the URL after `?`.

They are commonly used for:

- Searching
- Filtering
- Sorting
- Pagination

Example:

```text
/users?id=101
```

Here:

```text
id=101
```

is a query parameter.

---

## 🔹 Access Query Parameters

Express provides:

```js
req.query
```

Example:

```js
app.get("/users", (req, res) => {

    console.log(req.query);

    res.send("Users");
});
```

Request:

```text
/users?id=101
```

Output:

```js
{ id: "101" }
```

---

## 🔹 Access a Specific Parameter

```js
app.get("/users", (req, res) => {

    const id = req.query.id;

    res.send(`User ID: ${id}`);
});
```

Request:

```text
/users?id=101
```

Output:

```text
User ID: 101
```

---

## 🔹 Multiple Query Parameters

We can use multiple parameters with `&`.

```text
/users?name=Dharun&age=21
```

Code:

```js
app.get("/users", (req, res) => {

    const name = req.query.name;
    const age = req.query.age;

    res.json({
        name: name,
        age: age
    });
});
```

Response:

```json
{
    "name": "Dharun",
    "age": "21"
}
```

---

## 🔹 Search Example

```js
app.get("/products", (req, res) => {

    const search = req.query.search;

    res.send(`Searching for: ${search}`);
});
```

Request:

```text
/products?search=laptop
```

Output:

```text
Searching for: laptop
```

---

## 🔹 Filtering Example

```js
app.get("/products", (req, res) => {

    const category = req.query.category;

    res.send(`Category: ${category}`);
});
```

Request:

```text
/products?category=electronics
```

Output:

```text
Category: electronics
```

---

## 🔹 Pagination Example

Query parameters are commonly used for pagination.

```text
/products?page=2&limit=10
```

Code:

```js
app.get("/products", (req, res) => {

    const page = req.query.page;
    const limit = req.query.limit;

    res.json({
        page: page,
        limit: limit
    });
});
```

Response:

```json
{
    "page": "2",
    "limit": "10"
}
```

---

## 🔹 Query Parameter vs Route Parameter

### Route Parameter

```text
/users/101
```

```js
req.params.id
```

### Query Parameter

```text
/users?id=101
```

```js
req.query.id
```

| Route Parameter | Query Parameter |
|---|---|
| `/users/101` | `/users?id=101` |
| `req.params` | `req.query` |
| Part of route path | Comes after `?` |
| Usually identifies resource | Usually filters/searches/options |

---

## 🔹 Important Point

Query parameter values are generally received as **strings**.

Example:

```text
/products?page=2
```

```js
const page = Number(req.query.page);
```

Now:

```text
page → 2
```

as a number.

---

## 🎯 Interview Questions

### ❓ What are query parameters?

> Query parameters are values added to a URL after `?`, commonly used for filtering, searching, sorting, and pagination.

### ❓ How do you access query parameters in Express?

```js
req.query
```

### ❓ How do you pass multiple query parameters?

```text
/products?category=phone&sort=price
```

Parameters are separated using:

```text
&
```

### ❓ Difference between `req.params` and `req.query`?

> `req.params` contains values defined in the route path, while `req.query` contains values passed after `?` in the URL.

---

## 🧠 Quick Revision

```text
URL:
 /products?search=laptop&page=2

        ↓

req.query

        ↓

{
  search: "laptop",
  page: "2"
}
```

Remember:

```text
/:id       → req.params
?key=value → req.query
```

### ⭐ Interview One-Liner

> **Query parameters are URL parameters placed after `?` and are accessed in Express using `req.query`.**
