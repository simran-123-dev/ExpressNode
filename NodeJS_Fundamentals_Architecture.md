# Node.js Fundamentals & Architecture

## 1.1 What is Node.js? (The Runtime)

Historically, JavaScript was limited to web browsers such as Chrome and Firefox. In 2009, Ryan Dahl introduced Node.js by combining Chrome’s V8 Engine with a C++ library called **Libuv**.

### Definition

Node.js is a **cross-platform, open-source JavaScript runtime environment** that allows execution of JavaScript code outside a web browser.

### The V8 Engine

* Converts JavaScript into **machine code (binary)**
* Enables **fast execution** directly by the CPU
* Core reason behind Node.js performance

---

## 1.2 Single-Threaded Nature of Node.js

Traditional servers (Java, PHP):

* Create a **new thread per request**
* Heavy resource usage with many users

### Node.js Approach

* **Single-threaded architecture**
* Uses **non-blocking I/O**

### Key Idea

Instead of waiting for tasks (like file/database operations), Node.js:

* Delegates work to the system
* Continues handling other requests

This makes Node.js **highly scalable and efficient**.

---

## 1.3 Event Loop (Core Concept)

The **Event Loop** is the heart of Node.js. It enables asynchronous, non-blocking behavior.

### Working Mechanism

#### Step 1: Call Stack

* Executes synchronous code
* Example: `2 + 2`

#### Step 2: Node APIs (Background)

* Handles heavy operations:

  * Timers
  * File system
  * Database queries

#### Step 3: Callback Queue

* Stores completed async tasks

#### Step 4: Event Loop

* Continuously checks:

  * If Call Stack is empty → pushes tasks from queue to stack

### Summary

This system allows Node.js to handle **multiple operations efficiently using a single thread**.

---

## 1.4 Core Modules (Built-in Tools)

Node.js provides built-in modules that do not require installation.

---

### A. File System (fs Module)

Used for file operations such as create, read, update, delete.

```javascript
const fs = require('fs');

// Asynchronous Write (Non-blocking)
fs.writeFile('hello.txt', 'Learning Node.js Architecture', (err) => {
    if (err) throw err;
    console.log('File Created!');
});

console.log('I am printed first because Node is Async!');
```

**Key Point:**

* Non-blocking execution allows parallel processing

---

### B. Operating System (os Module)

Provides system-related information.

```javascript
const os = require('os');

console.log("Platform:", os.platform());
console.log("Architecture:", os.arch());
console.log("Free Memory:", os.freemem() / 1024 / 1024 / 1024, "GB");
```

---

## 1.5 Module System (CommonJS vs ES Modules)

Node.js supports two module systems:

---

### CommonJS (Default)

* Uses:

  * `require()`
  * `module.exports`

```javascript
const fs = require('fs');
```

---

### ES Modules (Modern Approach)

* Uses:

  * `import`
  * `export`

```javascript
import fs from 'fs';
```

### Requirement

To use ES Modules, add this in `package.json`:

```json
{
  "type": "module"
}
```

---

## Conclusion

Node.js is powerful because of:

* V8 Engine (fast execution)
* Single-threaded architecture
* Event Loop (non-blocking operations)
* Built-in modules
* Flexible module system

It is widely used for:

* Backend development
* APIs
* Real-time applications

---
