# Express.js Templating, MongoDB & Mongoose (CRUD Operations)

---

## 🧾 7. Templating Engines (Brief Overview)

Templating engines like **EJS** and **Pug** allow the server to dynamically inject data into HTML before sending it to the client.

---

### Why Use Templating Engines?

* Useful for **server-side rendered pages**
* Example:

  * Success page ("Email Sent")
  * Simple dashboards

---

### Why React Developers Usually Skip Them

* React handles UI on the frontend
* Backend (Node/Express) mainly sends:

  * JSON data instead of HTML

---

## 🗄️ 8. Database Integration: MongoDB & Mongoose

This forms the core of the **MERN Stack**.

---

## A. What is MongoDB?

MongoDB is a **NoSQL database**.

---

### Key Concepts

* Stores data in **Documents** (JSON-like format)
* Documents are grouped into **Collections**
* Flexible schema (unlike SQL tables)

---

### Example Structure

```json id="mongo1"
{
  "name": "John",
  "email": "john@example.com",
  "age": 25
}
```

---

## B. What is Mongoose?

Mongoose is an **ODM (Object Data Modeling) library** for MongoDB.

---

### Why Mongoose?

Problem:

* MongoDB allows storing anything → no structure

Solution:

* Mongoose enforces structure using **Schemas**

---

## 🛠️ Setting up Mongoose

---

### 1. Install Mongoose

```bash id="mg1"
npm install mongoose
```

---

### 2. Connect to MongoDB

```javascript id="mg2"
const mongoose = require('mongoose');

mongoose.connect('mongodb://127.0.0.1:27017/myDatabase')
  .then(() => console.log("Connected to MongoDB!"))
  .catch((err) => console.log("Connection Error:", err));
```

---

### 3. Create Schema & Model

```javascript id="mg3"
// models/User.js
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
    name: { type: String, required: true },
    email: { type: String, unique: true, required: true },
    age: Number,
    createdAt: { type: Date, default: Date.now }
});

module.exports = mongoose.model('User', userSchema);
```

---

## 🏗️ 8.1 CRUD Operations (Core of APIs)

CRUD = Create, Read, Update, Delete

---

### Create (POST)

```javascript id="crud1"
const User = require('./models/User');

app.post('/register', async (req, res) => {
    try {
        const newUser = new User(req.body);
        await newUser.save();

        res.status(201).json({
            message: "User Saved!",
            user: newUser
        });
    } catch (err) {
        res.status(400).json({ error: err.message });
    }
});
```

---

### Read (GET)

```javascript id="crud2"
app.get('/users', async (req, res) => {
    const users = await User.find();
    res.json(users);
});
```

---

### Update (PUT / PATCH)

```javascript id="crud3"
app.put('/user/:id', async (req, res) => {
    const updatedUser = await User.findByIdAndUpdate(
        req.params.id,
        req.body,
        { new: true }
    );

    res.json(updatedUser);
});
```

---

### Delete (DELETE)

```javascript id="crud4"
app.delete('/user/:id', async (req, res) => {
    await User.findByIdAndDelete(req.params.id);

    res.json({ message: "User Deleted" });
});
```

---

## Key Takeaways

* MongoDB stores flexible JSON-like data
* Mongoose enforces structure via schemas
* CRUD operations form the backbone of any API
* Express + MongoDB = scalable backend

---

## Conclusion

With this setup, you can:

* Build full REST APIs
* Store and manage user data
* Integrate with frontend frameworks like React

This is a critical step toward building:

* MERN stack projects
* Production-ready backend systems

---
