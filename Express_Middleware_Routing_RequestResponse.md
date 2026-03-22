# Express.js Middleware, Routing & Request-Response Handling

---

## 🟢 4. Middleware (The "Security Layer")

Middleware is a function that has access to:

* `req` (Request object)
* `res` (Response object)
* `next` (Function to pass control)

---

### How Middleware Works

1. Request comes in
2. Middleware executes
3. Calls `next()`
4. Next middleware or route handler runs
5. Response is sent

---

### Important Rule

⚠️ Always call `next()`
If not called → request will **hang indefinitely**

---

### Example: Custom Middleware

```javascript id="mid1"
const express = require('express');
const app = express();

// Application-level middleware
app.use((req, res, next) => {
    console.log(`${new Date().toISOString()} - ${req.method} ${req.url}`);
    next();
});

app.get('/dashboard', (req, res) => {
    res.send("Welcome to Dashboard");
});
```

---

## Types of Middleware

### 1. Application-level

* Runs for every request
* Example: `app.use(express.json())`

---

### 2. Route-level

* Runs only for specific routes

---

### 3. Built-in Middleware

* Provided by Express
* Example: `express.static()`

---

### 4. Third-party Middleware

* Installed via npm
* Examples:

  * `morgan` → logging
  * `cors` → cross-origin handling

---

### 5. Error-handling Middleware

* Always has **4 parameters**:

  * `(err, req, res, next)`

```javascript id="mid2"
app.use((err, req, res, next) => {
    res.status(500).json({ error: err.message });
});
```

---

## 🔗 5. Routing in Depth

For large applications, routes should be modularized instead of writing everything in one file.

---

### A. Route Parameters (`req.params`)

Used for dynamic values in URLs

```javascript id="route1"
app.get('/user/:id', (req, res) => {
    const userId = req.params.id;
    res.send(`Fetching data for User ID: ${userId}`);
});
```

---

### B. Query Parameters (`req.query`)

Used for filtering/searching

Example: `/search?name=iphone&color=black`

```javascript id="route2"
app.get('/search', (req, res) => {
    const { name, color } = req.query;
    res.json({ searchItem: name, filter: color });
});
```

---

### C. Express Router (Modular Routing)

Helps in organizing routes into separate files

---

#### Step 1: Create Route File

```javascript id="route3"
// routes/userRoutes.js
const express = require('express');
const router = express.Router();

router.get('/profile', (req, res) => res.send("User Profile"));
router.get('/settings', (req, res) => res.send("User Settings"));

module.exports = router;
```

---

#### Step 2: Use in Main File

```javascript id="route4"
const userRoutes = require('./routes/userRoutes');

app.use('/users', userRoutes);
```

### Result:

* `/users/profile`
* `/users/settings`

---

## 📦 6. Request & Response Handling

These methods are essential for backend-to-frontend communication.

---

### res.json()

* Sends JSON response
* Most common for APIs

```javascript id="res1"
res.json({ message: "Success" });
```

---

### res.send()

* Sends text or HTML

```javascript id="res2"
res.send("<h1>Hello</h1>");
```

---

### res.status()

* Sets HTTP status code

```javascript id="res3"
res.status(404).send("Not Found");
```

---

### res.sendFile()

* Sends files (images, PDFs, etc.)

```javascript id="res4"
res.sendFile(__dirname + '/file.pdf');
```

---

## Conclusion

* Middleware controls request flow
* Routing organizes endpoints efficiently
* Express Router enables modular architecture
* Response methods define how data is sent to clients

These concepts are critical for:

* API development
* Full-stack applications
* Backend interview preparation

---
