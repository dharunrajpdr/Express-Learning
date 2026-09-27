# 🔒 Password Hashing

## 🔹 What is Password Hashing?

**Password hashing** is the process of converting a password into a one-way hash before storing it in the database.

Instead of storing:

```text
123456
```

we store something like:

```text
$2b$10$...
```

---

## 🔹 Why Hash Passwords?

Passwords should **never be stored as plain text**.

```text
User Password
      ↓
   Hashing
      ↓
Password Hash
      ↓
   Database
```

If the database is exposed, storing plaintext passwords would directly reveal users' passwords.

---

## 🔹 Hashing vs Encryption

### Hashing

```text
Password → Hash
```

- One-way operation
- Used for password storage
- Cannot normally be reversed to the original password

### Encryption

```text
Data → Encrypted Data → Decrypted Data
```

- Reversible with the appropriate key
- Used when original data needs to be recovered

Easy memory:

```text
Hashing    → One Way
Encryption → Reversible
```

---

## 🔹 bcrypt

A common Node.js package for password hashing is:

```text
bcrypt
```

Install:

```bash
npm install bcrypt
```

Import:

```js
const bcrypt = require("bcrypt");
```

---

## 🔹 Hash a Password

```js
const password = "123456";

const hashedPassword = await bcrypt.hash(password, 10);

console.log(hashedPassword);
```

Here:

```text
123456 → Password
10     → Salt rounds
```

The resulting hash is stored in the database.

---

## 🔹 Compare Password

When the user logs in, we don't decrypt the stored hash.

Instead:

```js
const isMatch = await bcrypt.compare(
    password,
    hashedPassword
);
```

Example:

```js
const password = "123456";

const isMatch = await bcrypt.compare(
    password,
    hashedPassword
);

if (isMatch) {
    console.log("Password correct");
} else {
    console.log("Invalid password");
}
```

---

## 🔹 Registration Flow

```text
User enters password
        ↓
bcrypt.hash()
        ↓
Password Hash
        ↓
Save hash in Database
```

Example:

```js
app.post("/register", async (req, res) => {

    const { email, password } = req.body;

    const hashedPassword = await bcrypt.hash(password, 10);

    // Save email + hashedPassword to database

    res.status(201).json({
        message: "User registered"
    });
});
```

---

## 🔹 Login Flow

```text
User enters password
        ↓
Find user in database
        ↓
Get stored password hash
        ↓
bcrypt.compare()
        ↓
Match?
   ↙       ↘
 Yes       No
 ↓          ↓
Login     Reject
```

Example:

```js
app.post("/login", async (req, res) => {

    const { email, password } = req.body;

    // Example: user retrieved from database
    const user = {
        email: "dharun@example.com",
        passwordHash: "stored-hash"
    };

    const isMatch = await bcrypt.compare(
        password,
        user.passwordHash
    );

    if (!isMatch) {
        return res.status(401).json({
            message: "Invalid credentials"
        });
    }

    res.json({
        message: "Login successful"
    });
});
```

---

## 🔹 What is Salt?

A **salt** is random data used during password hashing.

It helps ensure that identical passwords do not result in identical stored hashes when properly salted.

With bcrypt:

```js
bcrypt.hash(password, 10);
```

bcrypt handles salt generation as part of the hashing process.

---

## 🔹 Important Security Points

```text
❌ Don't store plaintext passwords
❌ Don't put passwords inside JWT payloads
❌ Don't log user passwords
❌ Don't return password hashes to clients
```

Use:

```text
bcrypt
HTTPS
Secure environment configuration
Input validation
```

---

## 🎯 Interview Questions

### ❓ What is password hashing?

> Password hashing converts a password into a one-way hash so the original password is not stored directly in the database.

### ❓ Why use bcrypt?

> bcrypt is a password-hashing algorithm designed for securely hashing passwords and supporting salt generation.

### ❓ How do you verify a password?

```js
bcrypt.compare(password, hashedPassword);
```

### ❓ Can we decrypt a bcrypt hash?

> No. Password verification is performed by comparing the entered password with the stored hash.

### ❓ What is salt?

> A salt is random data used during hashing to make password hashes more resistant to certain attacks.

---

## 🧠 Quick Revision

```text
Registration:
Password
   ↓
bcrypt.hash()
   ↓
Hash
   ↓
Database
```

```text
Login:
Password
   ↓
bcrypt.compare()
   ↓
Stored Hash
   ↓
Match?
```

### ⭐ Interview One-Liner

> **Password hashing securely stores passwords as one-way hashes, and during login the entered password is verified using a function such as `bcrypt.compare()`.**
