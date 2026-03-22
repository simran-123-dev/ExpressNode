# Node.js Advanced Core Concepts

## 1.6 Buffers: Temporary Storage for Binary Data

In Node.js, a **Buffer** is a special object used to handle **binary (raw) data** such as images, videos, and network streams.

JavaScript originally handled only text data, so Node.js introduced Buffers to directly work with **memory at the byte level**.

### Key Characteristics

* **Fixed Size:** Once created, the size cannot be changed
* **Raw Memory Handling:** Stores data as a sequence of bytes (hexadecimal format)
* Used in:

  * File system operations
  * TCP streams
  * Binary data processing

### Example

```javascript id="buf1"
const buf = Buffer.from('Hello', 'utf-8');

console.log(buf);            // <Buffer 48 65 6c 6c 6f>
console.log(buf.toString()); // 'Hello'
```

---

## 1.7 Streams: Processing Data in Chunks

Streams allow data to be processed **piece by piece (chunks)** instead of loading everything into memory at once.

### Real-Life Analogy

Streaming a movie: You start watching without downloading the full file.

---

### Why Use Streams?

#### Memory Efficiency

* No need to load large files (e.g., 10GB) into RAM

#### Time Efficiency

* Start processing immediately with available chunks

---

### Types of Streams

1. **Readable Stream**

   * Used to read data
   * Example: `fs.createReadStream()`

2. **Writable Stream**

   * Used to write data
   * Example: `fs.createWriteStream()`

3. **Duplex Stream**

   * Can read and write
   * Example: network sockets

4. **Transform Stream**

   * Modifies data while reading/writing
   * Example: compression (zipping)

---

### pipe() Method

The `pipe()` method connects a **readable stream** directly to a **writable stream**.

### Example

```javascript id="stream1"
const fs = require('fs');

const readableStream = fs.createReadStream('./largeFile.txt');
const writableStream = fs.createWriteStream('./copyFile.txt');

// Efficient file copy using streams
readableStream.pipe(writableStream);
```

---

## 1.8 Creating a Server (Without Express)

Node.js provides the built-in **http module** to create web servers. This forms the foundation for frameworks like Express.js.

---

### Example: Basic HTTP Server

```javascript id="http1"
const http = require('http');

const server = http.createServer((req, res) => {

    if (req.url === '/') {
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.end('<h1>Welcome to the Home Page</h1>');

    } else if (req.url === '/api') {
        res.writeHead(200, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ message: "Hello from the API!" }));

    } else {
        res.writeHead(404, { 'Content-Type': 'text/plain' });
        res.end('404 Not Found');
    }
});

// Server listens on port 5000
server.listen(5000, () => {
    console.log('Server running at http://localhost:5000');
});
```

---

## Key Observations (Without Express)

### Manual Routing

* You must check routes using conditions like:

  * `if (req.url === '/')`

### Manual Headers

* Content types must be explicitly defined:

  * `text/html`
  * `application/json`

### More Boilerplate Code

* Writing APIs becomes repetitive and harder to scale

---

## Conclusion

These concepts strengthen your understanding of Node.js internals:

* Buffers → Handle binary data efficiently
* Streams → Process large data in chunks
* HTTP Module → Build servers from scratch

Understanding these fundamentals makes learning **Express.js much easier**, as Express abstracts many of these low-level details.

---
