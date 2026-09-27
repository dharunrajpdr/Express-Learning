# 🔐 Authentication

## 🔹 What is Authentication?

**Authentication** is the process of verifying **who the user is**.

Example:

```text
User enters email + password
          ↓
       Server
          ↓
   Verify credentials
          ↓
    Authentication
          ↓
      Login Success
```

---

## 🔹 Authentication vs Authorization

### Authentication

> **Who are you?**

Example:

```text
Login with email and password
```

### Authorization

> **What are you allowed to do?**

Example:

```text
Admin → Can delete users
User  → Cannot delete users
```

Easy memory:

```text
Authentication → Who?
Authorization  → What can you access?
```

---

## 🔹 Basic Login Flow

```text
React Frontend
      ↓
POST /login
      ↓
Express Backend
      ↓
Check email + password
      ↓
Create authenticated session/token
      ↓
Send response
      ↓
Frontend
```

---

## 🔹 Simple Login API

```js
app.post("/login", async (req, res) => {

    const { email, password } = req.body;

    // Normally, check user in database
    if (email === "dharun@example.com" && password === "1234") {

        res.json({
            message: "Login successful"
        });

    } else {

        res.status(401).json({
            message: "Invalid credentials"
        });
    }
});
```

> This is only a learning example. Real applications should never store or compare plaintext passwords like this.

---

## 🔹 Password Hashing

Passwords should **not** be stored as plain text.

Bad:

```text
password → 123456
```

Instead, applications store a **password hash**.

Example:

```text
Password
   ↓
Hashing Algorithm
   ↓
Password Hash
   ↓
Database
```

A common Node.js package for password hashing is:

```text
bcrypt
```

---

## 🔹 JWT Authentication

Another common authentication approach is **JWT (JSON Web Token)**.

Basic flow:

```text
Login
  ↓
Server verifies credentials
  ↓
Server creates JWT
  ↓
Client receives JWT
  ↓
Client sends JWT with protected requests
  ↓
Server verifies JWT
```

Example header:

```text
Authorization: Bearer <token>
```

JWT authentication is covered separately in the next topic.

---

## 🔹 Protected Route

Some APIs should only be accessible to authenticated users.

Example:

```text
GET /profile
```

Flow:

```text
Client
  ↓
Authentication information
  ↓
Auth Middleware
  ↓
Verify user
  ↓
Protected Route
```

---

## 🔹 Authentication in MERN

A common MERN authentication flow:

```text
React
  ↓
Login Form
  ↓
Axios / Fetch
  ↓
Express API
  ↓
MongoDB
  ↓
Verify User
  ↓
JWT / Cookie
  ↓
Authenticated User
```

---

## 🔹 Important Security Points

For real applications:

- Never store plaintext passwords.
- Hash passwords using a suitable password-hashing algorithm.
- Use HTTPS.
- Validate user input.
- Protect sensitive routes on the backend.
- Use secure cookie settings when using cookies.
- Do not expose secrets in frontend code.
- Handle authentication errors carefully.

---

## 🎯 Interview Questions

### ❓ What is authentication?

> Authentication is the process of verifying the identity of a user.

### ❓ What is authorization?

> Authorization determines what an authenticated user is allowed to access or perform.

### ❓ Why should passwords be hashed?

> Password hashing prevents applications from storing users' actual passwords directly in the database.

### ❓ What is JWT?

> JWT is a token format commonly used to carry authentication-related claims between a client and server.

### ❓ Where should authentication be enforced?

> Authentication and authorization must be enforced on the backend; frontend checks alone are not sufficient for security.

---

## 🧠 Quick Revision

```text
Authentication → Who are you?
Authorization  → What can you access?
```

Common flow:

```text
Login
  ↓
Verify Credentials
  ↓
Create Session / Token
  ↓
Authenticated Requests
  ↓
Protected Resources
```

### ⭐ Interview One-Liner

> **Authentication verifies the identity of a user, while authorization determines what that authenticated user is allowed to access or do.**
