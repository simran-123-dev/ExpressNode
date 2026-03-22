# Node.js NPM & Express.js Fundamentals

---

## ⚡ 2. NPM & Package Management

Before building large applications, we need a system to manage external libraries. **NPM (Node Package Manager)** is the world’s largest software registry and comes bundled with Node.js.

---

### npm init

* Command: `npm init`
* Creates a **package.json** file

### package.json

* Acts as the **identity of your project**
* Contains:

  * Project name
  * Version
  * Dependencies
  * Scripts

---

### package-lock.json

* Automatically generated file
* Locks exact versions of dependencies
* Ensures consistency across different systems

---

### Semantic Versioning (SemVer)

Example: `^4.17.1`

* **4 (Major):** Breaking changes
* **17 (Minor):** New features (backward compatible)
* **1 (Patch):** Bug fixes

---

### Installing Packages

```bash id="npm1"
npm install <package-name>
```

* Installs package into `node_modules`
* Adds dependency to `package.json`

⚠️ **Important:**
Never upload `node_modules` to GitHub
→ Add it to `.gitignore`

---

### npx (Node Package Executor)

```bash id="npm2"
npx create-react-app myApp
```

* Runs packages without installing them globally
* Useful for one-time executions

---

## 🌐 3. Creating a Server (Manual Way in Node.js)

Before using Express, it's important to understand how Node handles requests internally.

---

## Handling Requests & Responses (POST Example)

```javascript id="manual1"
const http = require('http');

const server = http.createServer((req, res) => {

    if (req.url === '/login' && req.method === 'POST') {
        let body = '';

        // Receiving data in chunks
        req.on('data', chunk => {
            body += chunk.toString();
        });

        // When data is fully received
        req.on('end', () => {
            const userData = JSON.parse(body);

            console.log("User logged in:", userData.username);

            res.writeHead(200, { 'Content-Type': 'application/json' });
            res.end(JSON.stringify({
                status: "Success",
                message: "Welcome!"
            }));
        });

    } else {
        res.writeHead(404);
        res.end("Route not found");
    }
});

server.listen(5000);
```

---

## Problems with Manual Approach

* Manual routing using `if-else`
* Handling data streams using `.on('data')`
* Manual JSON parsing
* Code becomes complex and unscalable

---

## 🚀 4. Express.js Fundamentals

Express simplifies all the complexities of Node's HTTP handling.

---

### What is Express?

Express is a **minimalist web framework** built on top of Node.js that simplifies:

* Routing
* Middleware handling
* Request & response processing

---

### Installation

```bash id="exp1"
npm install express
```

### Install Nodemon (Dev Tool)

```bash id="exp2"
npm install --save-dev nodemon
```

* Automatically restarts server on file changes

---

## Your First Express Server

```javascript id="exp3"
const express = require('express');
const app = express();

// Middleware to parse JSON
app.use(express.json());

// GET route
app.get('/', (req, res) => {
    res.status(200).send("Hello from Express!");
});

// POST route
app.post('/login', (req, res) => {
    const { username } = req.body;
    res.json({ message: `Welcome ${username}` });
});

// Start server
app.listen(5000, () => {
    console.log("Express Server Running...");
});
```

---

## Why Express is Better

### Automatic JSON Parsing

* No need for `.on('data')`

### Clean Routing

* Use `app.get()`, `app.post()` instead of `if-else`

### Readable Code

* Cleaner and scalable structure

---

## Conclusion

* NPM manages dependencies efficiently
* Manual Node.js server helps understand internals
* Express simplifies development significantly

Express is essential for building:

* REST APIs
* Backend servers
* Full-stack applications

---
