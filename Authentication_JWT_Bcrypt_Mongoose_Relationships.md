# Authentication, Authorization & Mongoose Relationships

---

## 🔐 9. Authentication & Authorization

Modern MERN applications use **stateless authentication** with **JWT (JSON Web Tokens)**.

### Key Idea

* Server does **not store session data**
* Client stores a **token (like an ID card)**
* Token is sent with every request

---

## A. Password Hashing (bcrypt)

Never store passwords in plain text.

---

### Why Hash Passwords?

* Protects user data if database is compromised
* Makes passwords unreadable using hashing + salt

---

### Example

```javascript id="auth1"
const bcrypt = require('bcryptjs');

// During Registration
const hashedPassword = await bcrypt.hash(req.body.password, 10);

// During Login
const isMatch = await bcrypt.compare(req.body.password, savedUser.password);
```

---

## B. JWT (JSON Web Token)

JWT consists of:

* Header
* Payload (contains user data like ID)
* Signature

---

### Generate Token (Login)

```javascript id="auth2"
const jwt = require('jsonwebtoken');

const token = jwt.sign(
    { id: user._id },
    process.env.JWT_SECRET,
    { expiresIn: '1h' }
);

res.json({ token });
```

---

### Middleware: Verify Token (Protect Routes)

```javascript id="auth3"
const verifyToken = (req, res, next) => {
    const token = req.headers['authorization'];

    if (!token) return res.status(403).send("Token required");

    try {
        const decoded = jwt.verify(token, process.env.JWT_SECRET);
        req.user = decoded; // Attach user info
        next();
    } catch (err) {
        res.status(401).send("Invalid Token");
    }
};
```

---

### Usage Example

```javascript id="auth4"
app.get('/dashboard', verifyToken, (req, res) => {
    res.send(`Welcome User ${req.user.id}`);
});
```

---

## 🗄️ 8.2 Database Relationships (Mongoose)

MongoDB supports two main ways to relate data:

---

### 1. Embedding

* Store related data inside the same document
* Best for:

  * Small, fixed data
  * Example: address inside user

---

### 2. Referencing

* Store `_id` of another document
* Best for:

  * Large or scalable data
  * Example: user → posts

---

## Example: User & Post Relationship

---

### Post Schema with Reference

```javascript id="rel1"
const mongoose = require('mongoose');

const postSchema = new mongoose.Schema({
    title: String,
    content: String,
    author: {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'User'
    }
});

module.exports = mongoose.model('Post', postSchema);
```

---

## Using populate()

When fetching data, references return only IDs.
Use `.populate()` to fetch actual related data.

---

### Example

```javascript id="rel2"
app.get('/all-posts', async (req, res) => {
    const posts = await Post.find()
        .populate('author', 'name email');

    res.json(posts);
});
```

---

## Key Takeaways

* Use **bcrypt** for password security
* Use **JWT** for stateless authentication
* Protect routes using middleware
* Use **referencing + populate()** for relationships

---

## Conclusion

With authentication and relationships implemented, you can:

* Build secure APIs
* Manage users and roles
* Create scalable database structures

These concepts are essential for:

* MERN stack projects
* Production-ready applications
* Backend interviews

---
