# Error Handling, Security, Performance & Deployment (Node.js + Express)

---

## ⚠️ 10. Error Handling

Error handling ensures your application does not crash and provides meaningful responses.

---

### Types of Errors

* **Operational Errors** (expected)

  * Invalid input
  * Database failure
* **Programming Errors**

  * Bugs in code

---

### Centralized Error Middleware

```javascript id="err1"
app.use((err, req, res, next) => {
    console.error(err.stack);

    res.status(err.status || 500).json({
        message: err.message || "Internal Server Error"
    });
});
```

---

### Async Error Handling

Use try-catch inside async functions:

```javascript id="err2"
app.get('/users', async (req, res, next) => {
    try {
        const users = await User.find();
        res.json(users);
    } catch (err) {
        next(err);
    }
});
```

---

### 404 Handler

```javascript id="err3"
app.use((req, res) => {
    res.status(404).json({ message: "Route Not Found" });
});
```

---

## 🛡️ 11. Security Best Practices

---

### 1. Helmet

Adds secure HTTP headers

```bash id="sec1"
npm install helmet
```

```javascript id="sec2"
const helmet = require('helmet');
app.use(helmet());
```

---

### 2. CORS

Allows cross-origin requests

```bash id="sec3"
npm install cors
```

```javascript id="sec4"
const cors = require('cors');
app.use(cors());
```

---

### 3. Rate Limiting

Prevents brute-force attacks

```bash id="sec5"
npm install express-rate-limit
```

```javascript id="sec6"
const rateLimit = require('express-rate-limit');

app.use(rateLimit({
    windowMs: 15 * 60 * 1000,
    max: 100
}));
```

---

### 4. Environment Variables

Store sensitive data securely

```bash id="sec7"
npm install dotenv
```

```javascript id="sec8"
require('dotenv').config();
```

---

### 5. Prevent Common Attacks

* XSS → sanitize inputs
* CSRF → use tokens
* Avoid exposing sensitive data

---

## ⚡ 12. Performance Optimization

---

### 1. Compression

```bash id="perf1"
npm install compression
```

```javascript id="perf2"
const compression = require('compression');
app.use(compression());
```

---

### 2. Caching (Basic Idea)

* Use Redis for caching frequently used data
* Reduces database load

---

### 3. Clustering

* Utilize multiple CPU cores
* Improves performance

---

## 🧪 13. Testing

---

### Tools

* **Jest** → Unit testing
* **Postman** → API testing

---

### Example

```javascript id="test1"
test('Sample Test', () => {
    expect(2 + 2).toBe(4);
});
```

---

## 🚀 14. Deployment & DevOps

---

### 1. Process Manager (PM2)

```bash id="dep1"
npm install pm2 -g
pm2 start server.js
```

---

### 2. Deployment Platforms

* Render
* Railway
* Vercel

---

### 3. Environment Setup

* Use `.env` file
* Set production variables

---

### 4. Basic CI/CD Idea

* Automate:

  * Testing
  * Deployment

---

## 📂 15. Project Structure (Best Practice)

```
project/
│
├── controllers/
├── routes/
├── models/
├── middleware/
├── config/
├── utils/
├── app.js
└── server.js
```

---

## 🎯 Final Conclusion

You now understand:

* Error handling (stable apps)
* Security (safe apps)
* Performance (fast apps)
* Deployment (live apps)

---

## 🚀 What Next?

Build real projects:

* REST API
* Authentication system
* Blog backend
* E-commerce backend
* Real-time app (chat)

---

**You now have a complete Node.js + Express + MongoDB backend roadmap.**

---
