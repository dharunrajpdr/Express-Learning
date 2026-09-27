# 📤 File Upload

## 🔹 What is File Upload?

**File upload** means sending a file from the client to the server.

Examples:

```text
Image
PDF
Video
Document
```

Basic flow:

```text
Frontend
   ↓
Select File
   ↓
HTTP Request
   ↓
Express Server
   ↓
Upload Middleware
   ↓
Storage
```

---

## 🔹 Why Do We Need Middleware?

Express does not directly handle `multipart/form-data` file uploads.

A commonly used package is:

```text
Multer
```

Install:

```bash
npm install multer
```

---

## 🔹 Basic File Upload

```js
const express = require("express");
const multer = require("multer");

const app = express();

const upload = multer({
    dest: "uploads/"
});

app.post("/upload", upload.single("file"), (req, res) => {

    console.log(req.file);

    res.json({
        message: "File uploaded successfully"
    });

});

app.listen(3000);
```

---

## 🔹 `upload.single()`

Used when uploading **one file**.

```js
upload.single("file")
```

Here:

```text
"file"
```

is the name of the form field.

The uploaded file is available through:

```js
req.file
```

---

## 🔹 Multiple Files

For multiple files with the same field name:

```js
app.post(
    "/upload",
    upload.array("files", 5),
    (req, res) => {

        console.log(req.files);

        res.json({
            message: "Files uploaded"
        });

    }
);
```

Here:

```text
Maximum files → 5
```

Uploaded files are available through:

```js
req.files
```

---

## 🔹 File Information

`req.file` can contain information such as:

```js
req.file.originalname
req.file.mimetype
req.file.size
req.file.filename
req.file.path
```

Example:

```js
app.post("/upload", upload.single("file"), (req, res) => {

    res.json({
        name: req.file.originalname,
        type: req.file.mimetype,
        size: req.file.size
    });

});
```

---

## 🔹 File Upload Request

For file uploads, the request usually uses:

```text
multipart/form-data
```

Example:

```text
POST /upload
Content-Type: multipart/form-data
```

The frontend can send a file using `FormData`.

Example:

```js
const formData = new FormData();

formData.append("file", selectedFile);

await axios.post(
    "http://localhost:3000/upload",
    formData
);
```

---

## 🔹 File Type Validation

We should validate uploaded files.

Example:

```js
const upload = multer({
    fileFilter: (req, file, cb) => {

        if (file.mimetype.startsWith("image/")) {
            cb(null, true);
        } else {
            cb(new Error("Only images are allowed"));
        }

    }
});
```

---

## 🔹 File Size Limit

We can limit file size.

```js
const upload = multer({
    limits: {
        fileSize: 2 * 1024 * 1024
    }
});
```

This allows files up to approximately:

```text
2 MB
```

---

## 🔹 Local Storage vs Cloud Storage

### Local Storage

Files are stored on the server.

```text
Client
  ↓
Express
  ↓
uploads/
```

### Cloud Storage

Files are stored using a cloud storage service.

```text
Client
  ↓
Backend
  ↓
Cloud Storage
```

Examples include:

```text
Cloudinary
Amazon S3
Google Cloud Storage
```

---

## 🔹 Important Security Points

For real applications:

```text
✓ Validate file type
✓ Limit file size
✓ Generate safe filenames
✓ Don't trust the original filename
✓ Restrict allowed file types
✓ Handle upload errors
✓ Use appropriate storage
```

Do not blindly allow every uploaded file.

---

## 🎯 Interview Questions

### ❓ What is Multer?

> Multer is Node.js middleware commonly used with Express to handle `multipart/form-data`, especially file uploads.

### ❓ What is `req.file`?

> `req.file` contains information about a single uploaded file.

### ❓ What is `req.files`?

> `req.files` contains information about multiple uploaded files.

### ❓ What is `multipart/form-data`?

> It is an HTTP content type commonly used for sending files and form data in the same request.

### ❓ How do you upload multiple files with Multer?

```js
upload.array("files", 5)
```

---

## 🧠 Quick Revision

```text
File Upload
    ↓
multipart/form-data
    ↓
Multer
    ↓
req.file / req.files
    ↓
Storage
```

Remember:

```text
One file   → upload.single()
Many files → upload.array()
```

### ⭐ Interview One-Liner

> **Multer is Express middleware used to handle `multipart/form-data` and process file uploads in Node.js applications.**
