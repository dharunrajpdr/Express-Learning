# 🔐 API Security

## 🔹 What is API Security?

**API Security** means protecting an API from unauthorized access, attacks, data leaks, and misuse.

Example:

```text
Client
   ↓
Authentication
   ↓
Authorization
   ↓
Input Validation
   ↓
API
   ↓
Database
```

---

## 🔹 Why is API Security Important?

Without proper security, attackers may:

```text
❌ Access private data
❌ Modify/delete data
❌ Steal credentials
❌ Upload malicious files
❌ Send too many requests
❌ Exploit invalid input
```

---

## 🔹 1. Authentication

Verify who the user is.

Example:

```text
Login
  ↓
Email + Password
  ↓
Verify User
  ↓
JWT / Session
  ↓
Authenticated User
```

Common methods:

```text
JWT
Sessions
Cookies
```

---

## 🔹 2. Authorization

Authentication tells us **who the user is**.

Authorization checks **what the user is allowed to do**.

Example:

```js
if (req.user.role !== "admin") {
    return res.status(403).json({
        message: "Access denied"
    });
}
```

Example:

```text
Admin → Delete User ✓
User  → Delete User ✗
```

---

## 🔹 3. Input Validation

Never trust data coming from the client.

Example:

```js
app.post("/users", (req, res) => {

    const { name, email } = req.body;

    if (!name || !email) {
        return res.status(400).json({
            message: "Name and email are required"
        });
    }

    res.json({
        message: "Valid data"
    });
});
```

For larger applications, validation libraries such as **Zod**, **Joi**, or **express-validator** can be used.

---

## 🔹 4. Password Security

Never store plaintext passwords.

Bad:

```text
password = 123456
```

Use password hashing:

```js
const hashedPassword = await bcrypt.hash(password, 10);
```

Verify during login:

```js
const isMatch = await bcrypt.compare(
    password,
    hashedPassword
);
```

---

## 🔹 5. HTTPS

Use **HTTPS** instead of HTTP for production APIs.

```text
HTTP
↓
Data can be exposed during transmission

HTTPS
↓
Encrypted connection
```

Example:

```text
https://api.example.com
```

HTTPS helps protect credentials, tokens, and other data while being transmitted.

---

## 🔹 6. Environment Variables

Do not hard-code sensitive information.

Bad:

```js
const JWT_SECRET = "my-secret-123";
```

Better:

`.env`

```text
JWT_SECRET=your-secret
MONGO_URI=your-database-url
```

Node.js:

```js
require("dotenv").config();

const secret = process.env.JWT_SECRET;
```

Also add:

```text
.env
```

to `.gitignore`.

---

## 🔹 7. Rate Limiting

Rate limiting restricts how many requests a client can make within a period.

Example:

```text
100 requests / 15 minutes
```

This can help reduce:

```text
Brute-force attempts
Abuse
Excessive requests
```

A commonly used package is:

```bash
npm install express-rate-limit
```

Example:

```js
const rateLimit = require("express-rate-limit");

const limiter = rateLimit({
    windowMs: 15 * 60 * 1000,
    max: 100
});

app.use(limiter);
```

---

## 🔹 8. CORS Configuration

Avoid blindly allowing every origin in production.

Instead of:

```js
app.use(cors());
```

you can specify allowed origins:

```js
app.use(cors({
    origin: "https://example.com"
}));
```

For credentialed requests, configure cookies and CORS together carefully.

---

## 🔹 9. Security Headers

Security-related HTTP headers can provide additional browser protections.

A commonly used Express package is:

```bash
npm install helmet
```

Example:

```js
const helmet = require("helmet");

app.use(helmet());
```

`helmet` configures several HTTP security headers.

---

## 🔹 10. Prevent Information Leakage

Avoid sending sensitive internal information to clients.

Bad:

```js
res.status(500).json({
    error: error.stack
});
```

Better:

```js
res.status(500).json({
    message: "Internal server error"
});
```

Detailed errors can be logged on the server while a safe message is returned to the client.

---

## 🔹 11. File Upload Security

If your API accepts files:

```text
✓ Validate file type
✓ Limit file size
✓ Generate safe filenames
✓ Restrict allowed extensions/types
✓ Store files safely
```

Do not blindly trust:

```js
req.file.originalname
```

or allow arbitrary executable content.

---

## 🔹 12. Protect Sensitive Routes

Example:

```js
app.get(
    "/profile",
    authenticateToken,
    (req, res) => {

        res.json({
            message: "Private profile"
        });

    }
);
```

Flow:

```text
Request
   ↓
Authentication Middleware
   ↓
Authorization
   ↓
Protected Route
   ↓
Response
```

---

## 🔹 13. MongoDB / Database Security

Important practices:

```text
✓ Validate input
✓ Use proper database permissions
✓ Protect database credentials
✓ Use environment variables
✓ Avoid exposing database directly to clients
```

Architecture:

```text
Frontend
   ↓
Express API
   ↓
Database
```

Not:

```text
Frontend
   ↓
Direct Database Access
```

---

## 🔹 14. Keep Dependencies Updated

Node.js applications depend on many packages.

Check for vulnerabilities:

```bash
npm audit
```

Update dependencies carefully:

```bash
npm update
```

Do not blindly update everything in a production application without testing.

---

## 🔹 15. Common API Security Checklist

```text
✓ Authentication
✓ Authorization
✓ Input Validation
✓ Password Hashing
✓ HTTPS
✓ Environment Variables
✓ Rate Limiting
✓ CORS Configuration
✓ Security Headers
✓ Safe Error Handling
✓ File Upload Validation
✓ Database Security
✓ Dependency Security
```

---

## 🔹 Simple Secure Express Structure

```js
const express = require("express");
const cors = require("cors");
const helmet = require("helmet");

const app = express();

app.use(helmet());

app.use(cors({
    origin: "https://example.com"
}));

app.use(express.json());

// Authentication middleware
// Validation
// Routes
// Error handling

app.listen(3000);
```

This is only a starting point; production security also depends on how authentication, cookies, validation, database access, file handling, and deployment are configured.

---

## 🎯 Interview Questions

### ❓ What is API security?

> API security is the practice of protecting APIs from unauthorized access, attacks, misuse, and data exposure.

### ❓ How can you secure an Express API?

> Use authentication, authorization, input validation, password hashing, HTTPS, rate limiting, secure CORS configuration, security headers, safe error handling, and protected environment variables.

### ❓ Why should passwords be hashed?

> To avoid storing users' actual passwords in the database.

### ❓ Why use Helmet?

> Helmet helps configure HTTP security headers for Express applications.

### ❓ What is rate limiting?

> Rate limiting restricts the number of requests a client can make within a specific time period.

### ❓ Should secrets be stored in frontend `.env` files?

> No. Frontend environment variables are generally exposed in the client bundle. Sensitive secrets should remain on the backend.

---

## 🧠 Quick Revision

```text
API Security
     ↓
Authentication
     ↓
Authorization
     ↓
Input Validation
     ↓
HTTPS
     ↓
Rate Limiting
     ↓
CORS
     ↓
Security Headers
     ↓
Safe Database Access
```

### ⭐ Interview One-Liner

> **API security protects backend APIs using authentication, authorization, validation, encryption, rate limiting, secure configuration, and safe data handling.**
