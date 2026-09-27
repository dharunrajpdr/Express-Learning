# 🔑 JWT

## 🔹 What is JWT?

**JWT** stands for **JSON Web Token**.

It is a compact token format commonly used for authentication between a client and server.

---

## 🔹 JWT Authentication Flow

```text
User Login
    ↓
Email + Password
    ↓
Server verifies user
    ↓
Server creates JWT
    ↓
Client receives JWT
    ↓
Client sends JWT with requests
    ↓
Server verifies JWT
    ↓
Access Protected Resource
```

---

## 🔹 JWT Structure

A JWT has 3 parts:

```text
Header.Payload.Signature
```

Example:

```text
xxxxx.yyyyy.zzzzz
```

### 1. Header

Contains information about the token, such as the signing algorithm.

### 2. Payload

Contains claims/data.

Example:

```json
{
    "userId": "101",
    "role": "user"
}
```

### 3. Signature

Used to verify that the token was created by a trusted server and has not been modified.

---

## 🔹 Install JWT Package

For Node.js:

```bash
npm install jsonwebtoken
```

Import:

```js
const jwt = require("jsonwebtoken");
```

---

## 🔹 Creating a JWT

```js
const token = jwt.sign(
    { userId: 101 },
    "my-secret-key",
    { expiresIn: "1h" }
);

console.log(token);
```

Here:

```text
userId → Payload
my-secret-key → Secret used for signing
1h → Token expiration
```

In a real application, the secret should come from a secure environment variable rather than being hard-coded.

---

## 🔹 Verifying a JWT

```js
const decoded = jwt.verify(
    token,
    "my-secret-key"
);

console.log(decoded);
```

If the token is valid, the decoded claims are returned.

If the token is invalid or expired, verification throws an error.

---

## 🔹 JWT Authentication Example

```js
const express = require("express");
const jwt = require("jsonwebtoken");

const app = express();

app.use(express.json());

const SECRET = "my-secret-key";

app.post("/login", (req, res) => {

    const { email, password } = req.body;

    // Example only
    if (email === "dharun@example.com" && password === "1234") {

        const token = jwt.sign(
            { email: email },
            SECRET,
            { expiresIn: "1h" }
        );

        return res.json({
            message: "Login successful",
            token: token
        });
    }

    res.status(401).json({
        message: "Invalid credentials"
    });
});
```

---

## 🔹 JWT Middleware

We can create middleware to protect routes.

```js
function authenticateToken(req, res, next) {

    const authHeader = req.headers.authorization;

    const token = authHeader && authHeader.split(" ")[1];

    if (!token) {
        return res.status(401).json({
            message: "Token required"
        });
    }

    try {

        const decoded = jwt.verify(token, SECRET);

        req.user = decoded;

        next();

    } catch (error) {

        return res.status(401).json({
            message: "Invalid or expired token"
        });
    }
}
```

---

## 🔹 Protected Route

```js
app.get("/profile", authenticateToken, (req, res) => {

    res.json({
        message: "Protected profile",
        user: req.user
    });

});
```

Request:

```text
GET /profile
```

Header:

```text
Authorization: Bearer <JWT_TOKEN>
```

Flow:

```text
Request
   ↓
authenticateToken
   ↓
Verify JWT
   ↓
req.user = decoded data
   ↓
next()
   ↓
/profile
```

---

## 🔹 JWT and Passwords

A JWT should **not contain the user's password**.

Bad payload:

```json
{
    "email": "dharun@example.com",
    "password": "123456"
}
```

Better:

```json
{
    "userId": 101,
    "role": "user"
}
```

Also remember:

> JWT payload is encoded, not encrypted by default.

Therefore, don't put sensitive secrets or passwords inside the payload.

---

## 🔹 JWT vs Session

| JWT | Session |
|---|---|
| Token contains claims | Server stores session state |
| Commonly sent with requests | Session ID commonly sent with requests |
| Server can verify token | Server looks up session |
| Often used in APIs | Common in traditional web applications |
| Can be stateless | Usually server-side state |

---

## 🎯 Interview Questions

### ❓ What is JWT?

> JWT is a compact token format commonly used for authentication and securely carrying claims between a client and server.

### ❓ What are the three parts of JWT?

```text
Header
Payload
Signature
```

### ❓ How do you verify a JWT?

```js
jwt.verify(token, secret);
```

### ❓ What is `Bearer` in an Authorization header?

```text
Authorization: Bearer <token>
```

`Bearer` indicates that the following value is the access token being presented with the request.

### ❓ Is JWT encrypted?

> Not by default. JWTs are typically signed and encoded, so their payload should not be treated as secret data.

---

## 🧠 Quick Revision

```text
Login
  ↓
Verify Credentials
  ↓
Create JWT
  ↓
Client stores/uses token
  ↓
Send Authorization header
  ↓
Server verifies JWT
  ↓
Protected Route
```

Remember:

```text
JWT
 ↓
Header + Payload + Signature
```

### ⭐ Interview One-Liner

> **JWT is a signed token format commonly used for authentication, where the server creates a token after login and verifies it on protected requests.**
