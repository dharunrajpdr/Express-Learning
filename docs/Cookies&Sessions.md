# 🍪 Cookies & Sessions

## 🔹 What are Cookies?

A **cookie** is a small piece of data stored by the browser and associated with a website.

Cookies are commonly used for:

- Authentication
- Sessions
- User preferences
- Remembering login state

Example:

```text
Browser
   ↓
Cookie
   ↓
Server
```

---

## 🔹 Setting a Cookie in Express

Express provides:

```js
res.cookie()
```

Example:

```js
app.get("/login", (req, res) => {

    res.cookie("username", "Dharun");

    res.send("Cookie created");

});
```

The browser can then store the cookie.

---

## 🔹 Reading Cookies

To easily read cookies in Express, we commonly use `cookie-parser`.

Install:

```bash
npm install cookie-parser
```

Use:

```js
const cookieParser = require("cookie-parser");

app.use(cookieParser());
```

Then:

```js
app.get("/profile", (req, res) => {

    console.log(req.cookies);

    res.send("Profile");
});
```

Access a specific cookie:

```js
const username = req.cookies.username;
```

---

## 🔹 Cookie Options

Cookies can have options.

```js
res.cookie("token", "abc123", {
    httpOnly: true,
    secure: true,
    maxAge: 60 * 60 * 1000
});
```

Important options:

```text
httpOnly → JavaScript cannot directly access the cookie
secure   → Cookie is sent only over HTTPS
maxAge   → Cookie lifetime
sameSite → Controls cross-site cookie behavior
```

---

## 🔹 What is a Session?

A **session** stores information about a user's login/session state on the server.

Example:

```text
User Login
    ↓
Server creates session
    ↓
Session ID
    ↓
Browser Cookie
    ↓
Future Requests
    ↓
Server finds session
```

The cookie commonly contains a **session identifier**, while the session data is maintained server-side.

---

## 🔹 Session Example

A common Express package is:

```bash
npm install express-session
```

Example:

```js
const session = require("express-session");

app.use(session({
    secret: "my-secret",
    resave: false,
    saveUninitialized: false
}));
```

Store data:

```js
app.get("/login", (req, res) => {

    req.session.userId = 101;

    res.send("Login successful");
});
```

Access session:

```js
app.get("/profile", (req, res) => {

    res.json({
        userId: req.session.userId
    });

});
```

> In production, session data should normally use a suitable persistent session store rather than relying on the default in-memory store.

---

## 🔹 Cookies vs Sessions

| Cookies | Sessions |
|---|---|
| Stored in browser | Session state is generally stored on server |
| Can store small pieces of data | Can store user session information |
| Sent with matching requests | Identified through a session ID |
| Can be used for preferences/auth | Commonly used for login state |

---

## 🔹 JWT + Cookies

JWT can also be stored in a cookie.

Example:

```js
res.cookie("token", token, {
    httpOnly: true,
    secure: true,
    sameSite: "strict"
});
```

Then the browser sends the cookie with appropriate requests.

This can be useful because an `HttpOnly` cookie cannot be directly read by JavaScript.

However, cookie-based authentication should be configured carefully, including appropriate `SameSite`, `Secure`, and CSRF protections.

---

## 🔹 Cookie vs LocalStorage

| Cookie | LocalStorage |
|---|---|
| Automatically sent with matching requests | Not automatically sent |
| Can be `HttpOnly` | Accessible through JavaScript |
| Can have `Secure` and `SameSite` settings | No `HttpOnly` |
| Common for cookie-based authentication | Common for client-side storage |

---

## 🎯 Interview Questions

### ❓ What is a cookie?

> A cookie is a small piece of data stored by the browser and associated with a website.

### ❓ What is a session?

> A session maintains user-specific state on the server, usually identified by a session ID stored in a cookie.

### ❓ What is an HttpOnly cookie?

> An HttpOnly cookie cannot be directly accessed through JavaScript.

### ❓ What does `secure: true` mean?

> It tells the browser to send the cookie only over HTTPS connections.

### ❓ Cookie vs Session?

> Cookies are stored on the client, while session state is generally maintained on the server and identified through a session ID.

---

## 🧠 Quick Revision

```text
Cookie
→ Stored in browser

Session
→ Session state stored on server

Session ID
→ Usually stored in browser cookie
```

Authentication flow:

```text
Login
  ↓
Create Session
  ↓
Session ID
  ↓
Cookie
  ↓
Future Request
  ↓
Server identifies Session
```

### ⭐ Interview One-Liner

> **Cookies store small data in the browser, while sessions maintain user-specific state on the server and commonly use a session ID stored in a cookie.**
