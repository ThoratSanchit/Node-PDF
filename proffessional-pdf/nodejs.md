# Chapter 1: Introduction to Node.js

## Table of Contents
- [What is Node.js?](#what-is-nodejs)
- [Why use Node.js?](#why-use-nodejs)
- [Installing Node.js & npm](#installing-nodejs--npm)
- [Understanding the Node.js Runtime and V8 Engine](#understanding-the-nodejs-runtime-and-v8-engine)
- [First Node.js Script](#first-nodejs-script)
- [Understanding process, __dirname, __filename](#understanding-process-__dirname-__filename)

---

## What is Node.js?

**Definition:**
Node.js is an open-source, cross-platform JavaScript runtime environment that allows you to run JavaScript code outside of a web browser, typically on the server side.

**Real-World Example:**
Imagine a busy coffee shop where a single barista takes orders, makes coffee, and serves customers. Instead of waiting for one coffee to finish before taking the next order, the barista takes multiple orders and prepares them as ingredients become available. Node.js works similarly by handling multiple requests efficiently without waiting for one to finish before starting another.

**Fun Fact:**
Node.js was created in 2009 by Ryan Dahl and has since become one of the most popular platforms for building scalable network applications.

### Key Points:
- **JavaScript Everywhere:** Use JavaScript for both frontend and backend development.
- **Single Language:** No need to learn different languages for different parts of your application.
- **Fast & Efficient:** Built on Google's V8 engine, which compiles JavaScript to machine code.

> **Analogy:** Like a coffee shop barista who multitasks, Node.js can handle multiple requests at once without getting stuck on one order.

---

## Why use Node.js?

**Definition:**
Node.js is designed for building scalable network applications due to its event-driven, non-blocking I/O model.

### 1. Event-Driven Architecture

**Definition:**
Event-driven architecture means the flow of the program is determined by events such as user actions, sensor outputs, or messages from other programs.

**Real-World Example:**
Think of a customer service call center. Calls (events) come in, and agents (handlers) respond as they become available, rather than making callers wait in a strict line.

```javascript
// Traditional approach (like a single phone line)
// One call at a time, others wait

// Node.js approach (like a call center)
// Multiple calls handled as agents become available
```

**What this means:** Node.js can handle multiple tasks at the same time, improving efficiency.

### 2. Non-Blocking I/O

**Definition:**
Non-blocking I/O allows other operations to continue while input/output operations are being performed.

**Real-World Example:**
Imagine you order food at a fast-food restaurant. Instead of waiting at the counter for your food, you get a number and sit down. When your food is ready, they call your number. This way, the restaurant can serve more people efficiently.

```javascript
// Blocking (old way)
const result = readFileSync('data.txt'); // Everything stops here
console.log('This waits until file is read');

// Non-blocking (Node.js way)
readFile('data.txt', (err, data) => {
    console.log('File read complete');
});
console.log('This runs immediately!');
```

### 3. Single-Threaded but Powerful

**Definition:**
Node.js uses a single-threaded event loop to handle multiple concurrent clients, making it lightweight and efficient.

**Real-World Example:**
A librarian (single thread) manages book checkouts for many students by quickly switching between them, rather than serving one student at a time until finished.

> **Why Single-Threaded?**: Like a librarian who can help many students by quickly switching between them, Node.js can handle many requests efficiently.

**Fun Fact:**
Despite being single-threaded, Node.js can handle thousands of concurrent connections thanks to its event-driven model.

---

## Installing Node.js & npm

**Definition:**
Node.js is the runtime, and npm (Node Package Manager) is the tool for managing JavaScript packages.

### Step 1: Download Node.js
1. Go to [nodejs.org](https://nodejs.org)
2. Download the **LTS version** (Long Term Support)
3. Run the installer

### Step 2: Verify Installation
Open your terminal/command prompt and type:

```bash
node --version
npm --version
```

You should see something like:
```
v18.17.0
9.6.7
```

### What is npm?

**Definition:**
npm is the default package manager for Node.js, used to install and manage libraries and tools for your projects.

**Real-World Example:**
npm is like an app store for JavaScript code, where you can download and manage reusable code packages for your projects.

```bash
# Installing a package
npm install express

# Creating a new project
npm init
```

---

## Understanding the Node.js Runtime and V8 Engine

### The V8 Engine

**Definition:**
The V8 engine is an open-source JavaScript engine developed by Google, used in Chrome and Node.js to execute JavaScript code.

**Real-World Example:**
V8 is like a high-performance car engine that makes your car (JavaScript code) run fast and efficiently.

**Fun Fact:**
V8 compiles JavaScript directly to machine code before executing it, making it extremely fast.

### Node.js Runtime Architecture

**Definition:**
The Node.js runtime provides the environment and tools needed to execute JavaScript code outside the browser.

```
┌─────────────────────────────────────┐
│           Your JavaScript Code      │
├─────────────────────────────────────┤
│           Node.js Runtime           │
│  ┌─────────────┐ ┌─────────────┐   │
│  │   V8 Engine │ │ Event Loop  │   │
│  └─────────────┘ └─────────────┘   │
├─────────────────────────────────────┤
│           Operating System          │
└─────────────────────────────────────┘
```

**Analogy:**
- **V8 Engine:** The car engine
- **Event Loop:** The driver who manages all the routes
- **Node.js Runtime:** The whole car system
- **Your Code:** The instructions for the trip

---

## First Node.js Script

### 1. Hello World!

**Definition:**
A simple script to print a message to the console, demonstrating how to run JavaScript with Node.js.

Create a file called `hello.js`:

```javascript
console.log("Hello, Node.js World!");
console.log("Welcome to the amazing world of backend development!");
```

Run it:
```bash
node hello.js
```

### 2. Creating a Simple Server

**Definition:**
A basic HTTP server in Node.js can respond to web requests, showing how Node.js can be used for web development.

**Real-World Example:**
Like opening a lemonade stand where you serve drinks (web pages) to customers (users) who visit your stand (server).

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end(`
        <html>
            <head>
                <title>My First Node.js Server</title>
            </head>
            <body>
                <h1>Welcome to My Node.js Server!</h1>
                <p>Your server is running successfully!</p>
                <p>Current time: ${new Date().toLocaleString()}</p>
            </body>
        </html>
    `);
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Server is open! Visit: http://localhost:${PORT}`);
    console.log(`Server started at: ${new Date().toLocaleString()}`);
});
```

**What this does:**
1. **Creates a server** (like opening a lemonade stand)
2. **Listens for requests** (like waiting for customers)
3. **Serves HTML content** (like serving drinks)
4. **Runs on port 3000** (like having a specific address)

### 3. Running Your Server

```bash
node server.js
```

Then open your browser and go to: `http://localhost:3000`

> **Pro Tip:** `localhost` means "this computer" - like saying "my house" instead of your full address.

---

## Understanding process, __dirname, __filename

### The `process` Object

**Definition:**
The `process` object provides information about, and control over, the current Node.js process.

**Real-World Example:**
The `process` object is like your computer's dashboard, showing details like your username, current directory, and environment.

```javascript
console.log('Process ID:', process.pid);
console.log('Node.js Version:', process.version);
console.log('Platform:', process.platform);
console.log('Current Directory:', process.cwd());
```

### __dirname and __filename

**Definition:**
`__dirname` is the directory name of the current module, and `__filename` is the file name of the current module.

**Real-World Example:**
`__dirname` is like your home address, and `__filename` is like your exact room number in your house.

```javascript
console.log('Current file location:', __filename);
console.log('Current folder location:', __dirname);
```

### Practical Example: File Paths

```javascript
const path = require('path');

console.log('File directory:', __dirname);
const dataFile = path.join(__dirname, 'data.txt');
console.log('Data file path:', dataFile);
console.log('File name:', path.basename(__filename));
console.log('File extension:', path.extname(__filename));
```

### Complete Example: File Explorer

```javascript
const fs = require('fs');
const path = require('path');

console.log('File Explorer Information:');
console.log('=============================');
console.log(`Current Directory: ${process.cwd()}`);
console.log(`Current File: ${__filename}`);
console.log(`File Directory: ${__dirname}`);
console.log(`File Name: ${path.basename(__filename)}`);
console.log(`File Extension: ${path.extname(__filename)}`);

fs.readdir(__dirname, (err, files) => {
    if (err) {
        console.error('Error reading directory:', err);
        return;
    }
    files.forEach(file => {
        const filePath = path.join(__dirname, file);
        const stats = fs.statSync(filePath);
        const type = stats.isDirectory() ? 'DIR' : 'FILE';
        console.log(`${type} ${file}`);
    });
});
```

---

## Summary

### What We Learned:
- **Node.js** is a JavaScript runtime for server-side development
- **Event-driven, non-blocking** architecture makes it super efficient
- **V8 engine** provides the power (like a sports car engine)
- **npm** is our package manager (like an online grocery store)
- **Simple servers** can be created with just a few lines of code
- **process, __dirname, __filename** help us navigate our application

### Key Analogies:
- **Node.js** = Multitasking barista
- **V8 Engine** = Car engine
- **npm** = App store for code
- **localhost** = Your house address
- **__dirname/__filename** = Home address and room number

### Next Steps:
In the next chapter, we'll explore **Node.js Core Modules** - the built-in tools that make Node.js so powerful!

---

## Practice Questions

1. What is Node.js and what problem does it solve?
2. Explain the difference between blocking and non-blocking I/O with an example.
3. What is the V8 engine and why is it important for Node.js?
4. How does event-driven architecture benefit Node.js applications?
5. What is npm and how is it used in Node.js projects?
6. Write a simple Node.js script that prints your name and the current time.
7. How do you create a basic HTTP server in Node.js?
8. What do `__dirname` and `__filename` represent in Node.js?
9. Describe a real-world analogy for how Node.js handles multiple requests.
10. List two fun facts about Node.js or its ecosystem.

---

**Ready for Chapter 2? Let's dive into the amazing world of Node.js Core Modules!** 

# Chapter 2: Node.js Core Modules

## Table of Contents
- [What are Core Modules?](#what-are-core-modules)
- [File System Module (fs)](#file-system-module-fs)
- [Path Module (path)](#path-module-path)
- [OS Module](#os-module)
- [Events Module and EventEmitter](#events-module-and-eventemitter)
- [HTTP Module](#http-module)
- [Reading/Writing Files: Async vs Sync](#readingwriting-files-async-vs-sync)
- [Using Callbacks with fs](#using-callbacks-with-fs)

---

## What are Core Modules?

**Definition:**
Core modules are built-in modules that come with Node.js installation and provide essential functionality for common programming tasks.

**Real-World Example:**
Think of core modules like the basic tools in a Swiss Army knife. Each tool has a specific purpose - a knife for cutting, scissors for trimming, a screwdriver for fixing. Similarly, each core module has a specific job in Node.js.

**Fun Fact:**
Node.js comes with over 20 core modules, each designed to handle specific tasks like file operations, networking, and system information.

### Key Points:
- **Built-in:** No need to install separately
- **Reliable:** Always available and well-tested
- **Fast:** Optimized for performance
- **Essential:** Used in almost every Node.js application

> **Analogy:** Core modules are like the basic ingredients in your kitchen - salt, pepper, oil - you always have them and use them in almost every dish.

---

## File System Module (fs)

**Definition:**
The `fs` module provides an API for interacting with the file system, allowing you to read, write, update, and delete files and directories.

**Real-World Example:**
The `fs` module is like a digital librarian who can help you find, read, write, and organize books (files) in a library (file system).

### Basic File Operations

```javascript
const fs = require('fs');

// Reading a file
fs.readFile('data.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error reading file:', err);
        return;
    }
    console.log('File content:', data);
});

// Writing to a file
fs.writeFile('output.txt', 'Hello, Node.js!', (err) => {
    if (err) {
        console.error('Error writing file:', err);
        return;
    }
    console.log('File written successfully!');
});
```

### Directory Operations

```javascript
const fs = require('fs');

// Creating a directory
fs.mkdir('my-folder', (err) => {
    if (err) {
        console.error('Error creating directory:', err);
        return;
    }
    console.log('Directory created successfully!');
});

// Reading directory contents
fs.readdir('.', (err, files) => {
    if (err) {
        console.error('Error reading directory:', err);
        return;
    }
    console.log('Files in current directory:', files);
});
```

**What this does:**
- **readFile:** Like opening a book and reading its contents
- **writeFile:** Like writing in a new notebook
- **mkdir:** Like creating a new folder in your computer
- **readdir:** Like looking at all files in a folder

---

## Path Module (path)

**Definition:**
The `path` module provides utilities for working with file and directory paths, handling cross-platform path differences.

**Real-World Example:**
The `path` module is like a GPS system that helps you navigate to different locations (files) regardless of which road system (operating system) you're using.

### Path Operations

```javascript
const path = require('path');

// Joining paths (works on any OS)
const fullPath = path.join(__dirname, 'data', 'users.json');
console.log('Full path:', fullPath);

// Getting file information
const filePath = '/home/user/documents/file.txt';
console.log('Directory:', path.dirname(filePath));
console.log('Filename:', path.basename(filePath));
console.log('Extension:', path.extname(filePath));

// Resolving relative paths
const absolutePath = path.resolve('./data/file.txt');
console.log('Absolute path:', absolutePath);
```

### Cross-Platform Path Handling

```javascript
const path = require('path');

// This works on Windows, Mac, and Linux
const userDataPath = path.join(__dirname, 'data', 'users', 'profile.json');

// Normalizing paths (removes extra slashes, etc.)
const normalizedPath = path.normalize('/home//user///documents/file.txt');
console.log('Normalized:', normalizedPath);

// Checking if path is absolute
console.log('Is absolute?', path.isAbsolute('/home/user/file.txt'));
console.log('Is absolute?', path.isAbsolute('./relative/path'));
```

**Key Benefits:**
- **Cross-platform:** Works on Windows, Mac, and Linux
- **Safe:** Handles path separators correctly
- **Clean:** Removes unnecessary slashes and dots

---

## OS Module

**Definition:**
The `os` module provides operating system-related utility methods and properties.

**Real-World Example:**
The `os` module is like a system dashboard that shows you information about your computer - memory usage, CPU info, network details, etc.

### System Information

```javascript
const os = require('os');

// Platform information
console.log('Operating System:', os.platform());
console.log('OS Type:', os.type());
console.log('OS Release:', os.release());

// CPU information
console.log('CPU Architecture:', os.arch());
console.log('Number of CPUs:', os.cpus().length);
console.log('CPU Model:', os.cpus()[0].model);

// Memory information
console.log('Total Memory:', (os.totalmem() / 1024 / 1024 / 1024).toFixed(2) + ' GB');
console.log('Free Memory:', (os.freemem() / 1024 / 1024 / 1024).toFixed(2) + ' GB');

// Network interfaces
console.log('Network Interfaces:', os.networkInterfaces());
```

### System Utilities

```javascript
const os = require('os');

// User information
console.log('Current User:', os.userInfo().username);
console.log('Home Directory:', os.homedir());

// System uptime
console.log('System Uptime:', (os.uptime() / 3600).toFixed(2) + ' hours');

// Load average (Unix-like systems)
console.log('Load Average:', os.loadavg());

// Endianness
console.log('Endianness:', os.endianness());
```

**Practical Use Cases:**
- **System monitoring:** Check memory and CPU usage
- **Cross-platform development:** Detect OS differences
- **Performance optimization:** Use system info for tuning

---

## Events Module and EventEmitter

**Definition:**
The `events` module provides the EventEmitter class, which is key to Node.js's event-driven architecture.

**Real-World Example:**
EventEmitter is like a radio station. The station (emitter) broadcasts signals (events), and listeners (receivers) tune in to hear specific programs.

### Basic EventEmitter Usage

```javascript
const EventEmitter = require('events');

// Create an event emitter
const myEmitter = new EventEmitter();

// Listen for an event
myEmitter.on('userLogin', (username) => {
    console.log(`User ${username} logged in!`);
});

// Emit an event
myEmitter.emit('userLogin', 'john_doe');
```

### Advanced Event Handling

```javascript
const EventEmitter = require('events');

class ChatRoom extends EventEmitter {
    constructor() {
        super();
        this.users = [];
    }

    addUser(username) {
        this.users.push(username);
        this.emit('userJoined', username);
        console.log(`Welcome, ${username}!`);
    }

    sendMessage(username, message) {
        this.emit('newMessage', { username, message, timestamp: new Date() });
    }
}

// Using the ChatRoom
const chat = new ChatRoom();

// Listen for events
chat.on('userJoined', (username) => {
    console.log(`🎉 ${username} joined the chat!`);
});

chat.on('newMessage', (data) => {
    console.log(`💬 ${data.username}: ${data.message}`);
});

// Trigger events
chat.addUser('Alice');
chat.addUser('Bob');
chat.sendMessage('Alice', 'Hello everyone!');
```

### Event Emitter Best Practices

```javascript
const EventEmitter = require('events');

class Database extends EventEmitter {
    constructor() {
        super();
        this.setMaxListeners(10); // Prevent memory leaks
    }

    connect() {
        // Simulate database connection
        setTimeout(() => {
            this.emit('connected', { timestamp: new Date() });
        }, 1000);
    }

    query(sql) {
        this.emit('query', { sql, timestamp: new Date() });
        // Simulate query execution
        setTimeout(() => {
            this.emit('result', { sql, data: 'Query results...' });
        }, 500);
    }
}

const db = new Database();

// Listen for database events
db.on('connected', (data) => {
    console.log('Database connected at:', data.timestamp);
});

db.on('query', (data) => {
    console.log('Executing query:', data.sql);
});

db.on('result', (data) => {
    console.log('Query result:', data.data);
});

// Use the database
db.connect();
setTimeout(() => db.query('SELECT * FROM users'), 1500);
```

---

## HTTP Module

**Definition:**
The `http` module provides functionality to create HTTP servers and make HTTP requests.

**Real-World Example:**
The `http` module is like a restaurant where you can be both a customer (making requests) and a waiter (serving requests to others).

### Creating a Basic HTTP Server

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    // Set response headers
    res.writeHead(200, { 'Content-Type': 'text/html' });
    
    // Handle different routes
    switch (req.url) {
        case '/':
            res.end(`
                <html>
                    <head><title>My Server</title></head>
                    <body>
                        <h1>Welcome to My Node.js Server!</h1>
                        <p>Current time: ${new Date().toLocaleString()}</p>
                        <a href="/about">About</a> | 
                        <a href="/contact">Contact</a>
                    </body>
                </html>
            `);
            break;
            
        case '/about':
            res.end(`
                <html>
                    <head><title>About</title></head>
                    <body>
                        <h1>About Us</h1>
                        <p>This is a simple Node.js server.</p>
                        <a href="/">Home</a>
                    </body>
                </html>
            `);
            break;
            
        case '/api/users':
            res.writeHead(200, { 'Content-Type': 'application/json' });
            res.end(JSON.stringify([
                { id: 1, name: 'John Doe' },
                { id: 2, name: 'Jane Smith' }
            ]));
            break;
            
        default:
            res.writeHead(404, { 'Content-Type': 'text/html' });
            res.end(`
                <html>
                    <head><title>404 Not Found</title></head>
                    <body>
                        <h1>404 - Page Not Found</h1>
                        <p>The page you're looking for doesn't exist.</p>
                        <a href="/">Go Home</a>
                    </body>
                </html>
            `);
    }
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`🚀 Server running at http://localhost:${PORT}`);
    console.log(`📅 Started at: ${new Date().toLocaleString()}`);
});
```

### Making HTTP Requests

```javascript
const http = require('http');

// Making a GET request
const options = {
    hostname: 'jsonplaceholder.typicode.com',
    port: 80,
    path: '/posts/1',
    method: 'GET'
};

const req = http.request(options, (res) => {
    let data = '';
    
    res.on('data', (chunk) => {
        data += chunk;
    });
    
    res.on('end', () => {
        console.log('Response:', JSON.parse(data));
    });
});

req.on('error', (err) => {
    console.error('Request error:', err);
});

req.end();
```

---

## Reading/Writing Files: Async vs Sync

**Definition:**
Node.js provides both synchronous and asynchronous methods for file operations. Asynchronous methods don't block the event loop, while synchronous methods do.

**Real-World Example:**
Think of it like ordering food at a restaurant:
- **Synchronous:** You wait at the counter until your food is ready (blocks everything else)
- **Asynchronous:** You get a number and sit down, they call you when ready (you can do other things)

### Synchronous File Operations

```javascript
const fs = require('fs');

// Synchronous reading (BLOCKS the event loop)
try {
    const data = fs.readFileSync('data.txt', 'utf8');
    console.log('File content (sync):', data);
} catch (err) {
    console.error('Error reading file:', err);
}

// Synchronous writing
try {
    fs.writeFileSync('output-sync.txt', 'Hello from sync!');
    console.log('File written synchronously');
} catch (err) {
    console.error('Error writing file:', err);
}
```

### Asynchronous File Operations

```javascript
const fs = require('fs');

// Asynchronous reading (NON-BLOCKING)
fs.readFile('data.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error reading file:', err);
        return;
    }
    console.log('File content (async):', data);
});

// Asynchronous writing
fs.writeFile('output-async.txt', 'Hello from async!', (err) => {
    if (err) {
        console.error('Error writing file:', err);
        return;
    }
    console.log('File written asynchronously');
});

console.log('This runs immediately!');
```

### Performance Comparison

```javascript
const fs = require('fs');

console.log('Starting file operations...');

// Synchronous operations
console.time('sync-operations');
try {
    const data1 = fs.readFileSync('file1.txt', 'utf8');
    const data2 = fs.readFileSync('file2.txt', 'utf8');
    console.log('Sync operations completed');
} catch (err) {
    console.error('Sync error:', err);
}
console.timeEnd('sync-operations');

// Asynchronous operations
console.time('async-operations');
let completed = 0;
const totalFiles = 2;

fs.readFile('file1.txt', 'utf8', (err, data) => {
    if (err) console.error('Error reading file1:', err);
    completed++;
    if (completed === totalFiles) {
        console.log('Async operations completed');
        console.timeEnd('async-operations');
    }
});

fs.readFile('file2.txt', 'utf8', (err, data) => {
    if (err) console.error('Error reading file2:', err);
    completed++;
    if (completed === totalFiles) {
        console.log('Async operations completed');
        console.timeEnd('async-operations');
    }
});
```

**Key Differences:**
- **Sync:** Simple to understand, but blocks everything
- **Async:** More complex, but doesn't block other operations
- **Performance:** Async is usually better for I/O operations

---

## Using Callbacks with fs

**Definition:**
Callbacks are functions passed as arguments to other functions, executed when the operation completes.

**Real-World Example:**
Callbacks are like leaving a message with a receptionist. You give them your phone number (callback) and they call you back when your appointment is ready.

### Basic Callback Pattern

```javascript
const fs = require('fs');

// Reading a file with callback
fs.readFile('data.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error reading file:', err);
        return;
    }
    console.log('File content:', data);
    
    // Writing to another file
    fs.writeFile('output.txt', data.toUpperCase(), (err) => {
        if (err) {
            console.error('Error writing file:', err);
            return;
        }
        console.log('File written successfully!');
    });
});
```

### Nested Callbacks (Callback Hell)

```javascript
const fs = require('fs');

// This can become hard to read with many nested callbacks
fs.readFile('user-data.txt', 'utf8', (err, userData) => {
    if (err) {
        console.error('Error reading user data:', err);
        return;
    }
    
    const users = JSON.parse(userData);
    
    fs.readFile('config.txt', 'utf8', (err, configData) => {
        if (err) {
            console.error('Error reading config:', err);
            return;
        }
        
        const config = JSON.parse(configData);
        
        fs.writeFile('report.txt', JSON.stringify({ users, config }), (err) => {
            if (err) {
                console.error('Error writing report:', err);
                return;
            }
            console.log('Report generated successfully!');
        });
    });
});
```

### Error Handling with Callbacks

```javascript
const fs = require('fs');

function processFile(filename, callback) {
    fs.readFile(filename, 'utf8', (err, data) => {
        if (err) {
            // Pass error to callback
            return callback(err);
        }
        
        try {
            // Process the data
            const processedData = data.toUpperCase();
            callback(null, processedData);
        } catch (error) {
            // Handle processing errors
            callback(error);
        }
    });
}

// Using the function
processFile('data.txt', (err, result) => {
    if (err) {
        console.error('Error processing file:', err);
        return;
    }
    console.log('Processed data:', result);
});
```

### File System Utilities with Callbacks

```javascript
const fs = require('fs');
const path = require('path');

function createUserProfile(username, callback) {
    const userDir = path.join(__dirname, 'users', username);
    
    // Create user directory
    fs.mkdir(userDir, (err) => {
        if (err && err.code !== 'EEXIST') {
            return callback(err);
        }
        
        // Create profile file
        const profilePath = path.join(userDir, 'profile.json');
        const profileData = {
            username: username,
            createdAt: new Date().toISOString(),
            lastLogin: null
        };
        
        fs.writeFile(profilePath, JSON.stringify(profileData, null, 2), (err) => {
            if (err) {
                return callback(err);
            }
            
            // Create settings file
            const settingsPath = path.join(userDir, 'settings.json');
            const settingsData = {
                theme: 'dark',
                notifications: true,
                language: 'en'
            };
            
            fs.writeFile(settingsPath, JSON.stringify(settingsData, null, 2), (err) => {
                if (err) {
                    return callback(err);
                }
                
                callback(null, {
                    message: 'User profile created successfully',
                    profilePath: profilePath,
                    settingsPath: settingsPath
                });
            });
        });
    });
}

// Using the function
createUserProfile('john_doe', (err, result) => {
    if (err) {
        console.error('Error creating user profile:', err);
        return;
    }
    console.log('Success:', result);
});
```

---

## Summary

### What We Learned:
- **Core modules** are built-in tools for common tasks
- **fs module** handles file and directory operations
- **path module** manages file paths cross-platform
- **os module** provides system information
- **events module** powers Node.js's event-driven architecture
- **http module** creates servers and makes requests
- **Async vs Sync** operations affect performance
- **Callbacks** handle asynchronous operations

### Key Analogies:
- **Core modules** = Swiss Army knife tools
- **fs module** = Digital librarian
- **path module** = GPS for files
- **os module** = System dashboard
- **EventEmitter** = Radio station
- **http module** = Restaurant (customer and waiter)
- **Async vs Sync** = Restaurant ordering methods
- **Callbacks** = Receptionist messages

### Best Practices:
- **Use async operations** for I/O to avoid blocking
- **Handle errors properly** in callbacks
- **Use path.join()** for cross-platform compatibility
- **Set up event listeners** before emitting events
- **Avoid callback hell** with proper structure

### Next Steps:
In the next chapter, we'll explore **NPM and Package Management** - how to use external libraries and manage dependencies!

---

## Practice Questions

1. What are core modules and why are they important in Node.js?
2. Explain the difference between synchronous and asynchronous file operations with examples.
3. How does the EventEmitter class work? Provide a real-world example.
4. What is the purpose of the path module and why is it useful?
5. How would you create a basic HTTP server using the http module?
6. What information can you get from the os module?
7. Explain the callback pattern and provide an example with file operations.
8. How do you handle errors in asynchronous operations with callbacks?
9. What is "callback hell" and how can it be avoided?
10. Create a simple file system utility that reads a JSON file, modifies it, and writes it back.

---

**Ready for Chapter 3? Let's explore the amazing world of NPM and Package Management!** 

# Chapter 3: Asynchronous Programming in Node.js (Detailed)

## Table of Contents
- [1. Synchronous vs Asynchronous](#1-synchronous-vs-asynchronous)
- [2. Callbacks in Node.js](#2-callbacks-in-nodejs)
- [3. Callback Hell and How to Avoid It](#3-callback-hell-and-how-to-avoid-it)
- [4. Promises: then, catch, and Chaining](#4-promises-then-catch-and-chaining)
- [5. async/await Usage and Best Practices](#5-asyncawait-usage-and-best-practices)
- [6. Error Handling with try/catch](#6-error-handling-with-trycatch)

---

## 1. Synchronous vs Asynchronous

###  Definition of Synchronous Code (Blocking Behavior)
Synchronous code executes one operation at a time. Each line waits for the previous one to finish before running. This is called "blocking" because the program is blocked until the current task completes.

###  Definition of Asynchronous Code (Non-Blocking Behavior)
Asynchronous code allows the program to start a task and move on to the next one before the previous task finishes. This is called "non-blocking" because the program doesn't wait for the task to complete.

###  Real-World Analogy
- **Synchronous:** Like a single waiter who takes one order, serves it, and only then takes the next order.
- **Asynchronous:** Like a self-service restaurant where you order food, get a buzzer, and sit down. When your food is ready, the buzzer rings, and you pick it up. The staff can serve many people at once!

###  Examples in Node.js

#### Synchronous Example: `fs.readFileSync()`
```javascript
const fs = require('fs');
const data = fs.readFileSync('data.txt', 'utf8');
console.log('File contents:', data);
console.log('This line waits until the file is read.');
```

#### Asynchronous Example: `fs.readFile()`
```javascript
const fs = require('fs');
fs.readFile('data.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log('File contents:', data);
});
console.log('This line runs immediately!');
```

###  JavaScript Event Loop Basics
The event loop is the mechanism that allows Node.js to handle many operations at once. It checks for completed tasks and runs their callbacks when ready.

**Analogy:** The event loop is like a manager who keeps checking if any orders are ready to be served and calls out to the customer when their food is done.

###  Use Cases and Importance of Async Behavior in Servers
- Handling many users at once (e.g., web servers)
- Reading files, databases, or APIs without blocking other tasks
- Improving performance and responsiveness

---

## 2. Callbacks in Node.js

###  What is a Callback Function?
A callback is a function passed as an argument to another function, to be called when a task is finished.

###  Structure and Syntax of Callbacks
```javascript
function doSomethingAsync(callback) {
  setTimeout(() => {
    callback('Task complete!');
  }, 1000);
}

doSomethingAsync((message) => {
  console.log(message);
});
```

###  Node-Style Callbacks (`function(err, result)`)
Node.js uses a standard callback pattern: the first argument is an error (if any), and the second is the result.

```javascript
fs.readFile('data.txt', 'utf8', function(err, data) {
  if (err) {
    console.error('Error:', err);
    return;
  }
  console.log('Data:', data);
});
```

###  Example: Using `fs.readFile()` with a Callback
See above.

###  Callback in User-Defined Functions
```javascript
function add(a, b, callback) {
  setTimeout(() => {
    callback(null, a + b);
  }, 500);
}

add(2, 3, (err, result) => {
  if (err) return console.error(err);
  console.log('Sum:', result);
});
```

###  Advantages of Using Callbacks
- Non-blocking: Other code can run while waiting
- Flexible: Can be used for many async tasks
- Foundation for more advanced async patterns

---

## 3. Callback Hell and How to Avoid It

###  What is Callback Hell ("Pyramid of Doom")?
Callback hell happens when callbacks are nested inside callbacks, making code hard to read and maintain.

###  Code Example Showing Nested Callbacks
```javascript
fs.readFile('file1.txt', 'utf8', (err, data1) => {
  if (err) return console.error(err);
  fs.readFile('file2.txt', 'utf8', (err, data2) => {
    if (err) return console.error(err);
    fs.readFile('file3.txt', 'utf8', (err, data3) => {
      if (err) return console.error(err);
      console.log(data1, data2, data3);
    });
  });
});
```

###  Problems with Readability, Maintainability, Debugging
- Hard to read (deeply indented)
- Difficult to debug
- Hard to add or change logic

###  Solutions
#### Using Named Functions
```javascript
function handleFile3(err, data3) {
  if (err) return console.error(err);
  console.log('All files read!');
}
function handleFile2(err, data2) {
  if (err) return console.error(err);
  fs.readFile('file3.txt', 'utf8', handleFile3);
}
fs.readFile('file2.txt', 'utf8', handleFile2);
```

#### Modularizing Callback Logic
Move each step into its own function or module for clarity.

#### Transitioning to Promises
Promises flatten the structure and make code easier to follow (see next section).

---

## 4. Promises: then, catch, and Chaining

###  What is a Promise in JavaScript?
A Promise is an object representing the eventual completion (or failure) of an asynchronous operation.

###  States of a Promise: Pending, Fulfilled, Rejected
- **Pending:** Still working
- **Fulfilled:** Completed successfully
- **Rejected:** Failed with an error

###  Creating a New Promise Manually
```javascript
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Done!');
  }, 1000);
});
```

###  Consuming Promises Using `.then()`, `.catch()`, `.finally()`
```javascript
myPromise
  .then(result => {
    console.log('Success:', result);
  })
  .catch(error => {
    console.error('Error:', error);
  })
  .finally(() => {
    console.log('Cleanup done.');
  });
```

###  Chaining Multiple `.then()` Calls
```javascript
function asyncAdd(a, b) {
  return new Promise(resolve => setTimeout(() => resolve(a + b), 500));
}

asyncAdd(2, 3)
  .then(sum => {
    console.log('Sum:', sum);
    return asyncAdd(sum, 4);
  })
  .then(newSum => {
    console.log('New Sum:', newSum);
  });
```

###  Avoiding Callback Hell with Promises
Promises allow you to chain operations instead of nesting them.

###  Real-Life Example: Reading a File and Processing Data
```javascript
const fs = require('fs').promises;

fs.readFile('data.txt', 'utf8')
  .then(data => {
    console.log('File:', data);
    return data.toUpperCase();
  })
  .then(upper => {
    console.log('Uppercase:', upper);
  })
  .catch(err => {
    console.error('Error:', err);
  });
```

---

## 5. async/await Usage and Best Practices

###  What are async and await?
`async` and `await` are keywords that make working with Promises easier, allowing you to write asynchronous code that looks synchronous.

###  Converting Promise-Based Code into async/await
```javascript
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function main() {
  console.log('Start');
  await delay(1000);
  console.log('After 1 second');
}

main();
```

###  Cleaner Syntax with async Functions
Async functions let you use `await` inside them for a more readable flow.

###  Awaiting Multiple Promises (e.g., `await Promise.all()`)
```javascript
async function runTasks() {
  const [a, b] = await Promise.all([
    delay(500),
    delay(1000)
  ]);
  console.log('Both tasks done!');
}
```

###  Error Handling Using try/catch
```javascript
async function fetchData() {
  try {
    const data = await delay(500);
    console.log('Data:', data);
  } catch (err) {
    console.error('Error:', err);
  }
}
```

###  Best Practices
- Always use try/catch for error handling
- Avoid blocking code (like heavy loops) inside async functions
- Use `await` only when necessary (don’t block parallel tasks)
- Keep async functions small and modular

---

## 6. Error Handling with try/catch

###  Catching Synchronous Errors
```javascript
try {
  throw new Error('Oops!');
} catch (err) {
  console.error('Caught:', err.message);
}
```

###  Catching Asynchronous Errors Inside async/await
```javascript
async function failAsync() {
  throw new Error('Async error!');
}

(async () => {
  try {
    await failAsync();
  } catch (err) {
    console.error('Caught async error:', err.message);
  }
})();
```

###  Example with Rejected Promises
```javascript
Promise.reject(new Error('Promise failed!'))
  .catch(err => {
    console.error('Promise error:', err.message);
  });
```

###  Nested try/catch Blocks
```javascript
async function outer() {
  try {
    await inner();
  } catch (err) {
    console.error('Outer error:', err.message);
  }
}
async function inner() {
  try {
    throw new Error('Inner error!');
  } catch (err) {
    console.error('Inner caught:', err.message);
    throw err; // rethrow
  }
}
```

###  Throwing Custom Errors
```javascript
function doSomethingBad() {
  throw new Error('Custom error!');
}
```

###  Logging and Returning Meaningful Error Messages
Always log errors with context and return user-friendly messages.

###  Optional: Using Middleware for Centralized Error Handling (Preview for Express)
In Express.js, you can use middleware to handle errors in one place:
```javascript
app.use((err, req, res, next) => {
  console.error('Central error handler:', err);
  res.status(500).send('Something broke!');
});
```

---

## Summary

### What We Learned
- The difference between synchronous and asynchronous code
- How callbacks work and their structure
- What callback hell is and how to avoid it
- How Promises and async/await simplify async code
- Best practices for error handling

### Key Analogies
- **Synchronous:** Waiter serves one at a time
- **Asynchronous:** Self-service restaurant
- **Callback:** Pizza order and callback phone number
- **Callback Hell:** Pyramid of Doom
- **Promise:** Package tracking number
- **async/await:** Waiting for coffee
- **try/catch:** Wearing a helmet

### Next Steps
In the next chapter, we’ll explore more advanced Node.js features and how to build robust applications!

---

## Practice Questions
1. What is the difference between synchronous and asynchronous code?
2. Give a real-world analogy for asynchronous behavior.
3. What is a callback function and how is it used in Node.js?
4. What is callback hell and how can you avoid it?
5. How do Promises help manage async code?
6. How does async/await improve code readability?
7. How do you handle errors in async functions?
8. What is the purpose of `Promise.all()`?
9. Give an example of a custom error.
10. How can Express middleware help with error handling?

---

**Ready for the next chapter 4? Let's Getting Started with Express.js!** 

# Chapter 4: Getting Started with Express.js

## Table of Contents
- [What is Express.js?](#what-is-expressjs)
- [Why Use Express.js?](#why-use-expressjs)
- [Installing Node.js & Express](#installing-nodejs--express)
- [Your First Express App](#your-first-express-app)
- [Understanding Routing (GET, POST, PUT, DELETE)](#understanding-routing-get-post-put-delete)
- [Handling Requests and Responses](#handling-requests-and-responses)
- [Middleware in Express.js](#middleware-in-expressjs)
- [Serving Static Files](#serving-static-files)
- [Route Parameters and Query Strings](#route-parameters-and-query-strings)
- [Organizing Your Express App](#organizing-your-express-app)
- [Summary](#summary)
- [Practice Questions](#practice-questions)

---

## What is Express.js?

**Definition:**
Express.js is a simple and flexible tool that helps you build web servers and websites using JavaScript and Node.js. It makes it much easier to handle web requests and responses.

**Real-World Example:**
Imagine you want to open a lemonade stand. Node.js gives you the kitchen and ingredients, but you have to do everything yourself. Express.js is like having a set of ready-made tools and recipes, so you can serve your lemonade to customers quickly and easily.

**Fun Fact:**
Express.js is one of the most popular frameworks for building web apps in JavaScript!

### Key Points:
- Makes web server code much shorter and easier
- Lets you handle different web addresses (routes) simply
- Works with many extra tools (middleware)

> **Analogy:** Express.js is like a food truck kit for building web servers—fast, flexible, and ready to go!

---

## Why Use Express.js?

**Definition:**
Express.js helps you build web apps and APIs quickly, without having to write a lot of repetitive code.

**Real-World Example:**
Building a website with just Node.js is like building a house from scratch. With Express.js, you get pre-made walls, doors, and windows, so you can focus on making your house unique.

### Features of Express
- Easy routing (handling different URLs)
- Middleware support (add features like logging, security, etc.)
- Serve static files (like images, CSS, HTML)
- Works with databases and other tools

### Comparison: Express.js vs Node.js HTTP Module
| Feature                | Node.js HTTP Module | Express.js           |
|------------------------|--------------------|----------------------|
| Routing                | Manual             | Built-in, easy       |
| Middleware             | Manual             | Built-in, easy       |
| Static File Serving    | Manual             | Built-in             |
| Code Length            | Long               | Short                |
| Plugins                | Few                | Many                 |

### Real-World Use Cases
- Websites and blogs
- Online stores
- Chat apps
- REST APIs for mobile apps

### Benefits
- Saves time
- Easy to learn
- Huge community and lots of help online

---

## Installing Node.js & Express

**Definition:**
Node.js lets you run JavaScript on your computer. Express.js is a tool you add to Node.js projects.

### Step 1: Install Node.js
Go to [nodejs.org](https://nodejs.org) and download the LTS version. Install it on your computer.

### Step 2: Check Node.js and npm
Open your terminal or command prompt and type:
```bash
node -v
npm -v
```
You should see version numbers.

### Step 3: Create a New Project
```bash
mkdir my-express-app
cd my-express-app
npm init -y
```

### Step 4: Install Express
```bash
npm install express
```

---

## Your First Express App

**Definition:**
An Express app is a program that listens for web requests and sends back responses.

**Real-World Example:**
Like a lemonade stand that waits for customers and gives them drinks when they ask.

### Step-by-Step Example
Create a file called `app.js`:
```javascript
// 1. Import express
const express = require('express');
// 2. Create an app
const app = express();
// 3. Set a port number
const PORT = 3000;
// 4. Define a route for the homepage
app.get('/', (req, res) => {
  res.send('Hello, Express!');
});
// 5. Start the server
app.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`);
});
```

**How to Run:**
```bash
node app.js
```
Go to `http://localhost:3000` in your browser. You should see "Hello, Express!"

**Fun Fact:**
You can use a tool called `nodemon` to restart your server automatically when you make changes:
```bash
npm install -g nodemon
nodemon app.js
```

---

## Understanding Routing (GET, POST, PUT, DELETE)

**Definition:**
Routing means deciding what to do when someone visits a certain web address (URL) or sends data to your server.

**Real-World Example:**
Like a receptionist who tells visitors where to go in a building.

### Basic Routes
```javascript
// GET request (read data)
app.get('/hello', (req, res) => {
  res.send('Hello, GET!');
});
// POST request (add data)
app.post('/hello', (req, res) => {
  res.send('Hello, POST!');
});
// PUT request (update data)
app.put('/hello', (req, res) => {
  res.send('Hello, PUT!');
});
// DELETE request (remove data)
app.delete('/hello', (req, res) => {
  res.send('Hello, DELETE!');
});
```

### Sending Responses
- `res.send()` – send text or HTML
- `res.json()` – send JSON data
- `res.status()` – set HTTP status code

### Testing Routes
You can use tools like **Postman** (a free app) or the command line tool **curl**:
```bash
curl http://localhost:3000/hello
curl -X POST http://localhost:3000/hello
```

---

## Handling Requests and Responses

**Definition:**
When someone visits your site or sends data, Express gives you two objects: `req` (the request) and `res` (the response).

**Real-World Example:**
A customer (request) asks for lemonade, and you (response) give it to them.

### Getting Data from Requests
- **Query string:** `/search?term=express`
  ```javascript
  app.get('/search', (req, res) => {
    const term = req.query.term;
    res.send(`You searched for: ${term}`);
  });
  ```
- **URL parameter:** `/user/123`
  ```javascript
  app.get('/user/:id', (req, res) => {
    const userId = req.params.id;
    res.send(`User ID: ${userId}`);
  });
  ```
- **Request body:** (needs express.json() middleware)
  ```javascript
  app.use(express.json());
  app.post('/profile', (req, res) => {
    const { name, age } = req.body;
    res.send(`Name: ${name}, Age: ${age}`);
  });
  ```

### Sending Responses
- `res.send()` – send text/HTML
- `res.json()` – send JSON
- `res.status().send()` – set status and send
- `res.redirect()` – send to another page

```javascript
app.get('/redirect', (req, res) => {
  res.redirect('/hello');
});
```

---

## Middleware in Express.js

**Definition:**
Middleware is extra code that runs before your main route code. It can check things, change data, or add features.

**Real-World Example:**
Like a security guard who checks visitors before they enter a building.

### Application-level Middleware
```javascript
// Logger middleware (runs for every request)
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next(); // Go to the next step
});
```

### Router-level Middleware
```javascript
const router = require('express').Router();
router.use((req, res, next) => {
  console.log('Router-level middleware');
  next();
});
router.get('/test', (req, res) => res.send('Router test'));
app.use('/api', router);
```

### Built-in Middleware
- `express.static()` – serve static files
- `express.json()` – read JSON data
- `express.urlencoded()` – read form data

### Third-party Middleware
- **morgan:** Logging
- **cors:** Allow requests from other sites
- **helmet:** Security

```bash
npm install morgan cors helmet
```
```javascript
const morgan = require('morgan');
const cors = require('cors');
const helmet = require('helmet');
app.use(morgan('dev'));
app.use(cors());
app.use(helmet());
```

---

## Serving Static Files

**Definition:**
Static files are things like HTML, CSS, images, and JavaScript files that don’t change.

**Real-World Example:**
Like a brochure rack in a lobby—anyone can take a brochure (file) without asking.

### How to Serve Static Files
```javascript
app.use(express.static('public'));
```

### Setting up a public/ Folder
```
my-express-app/
├── public/
│   ├── index.html
│   ├── style.css
│   └── images/
│       └── logo.png
```

### Customizing the Static Path
```javascript
app.use('/static', express.static('public'));
// Now /static/index.html serves public/index.html
```

---

## Route Parameters and Query Strings

**Definition:**
Route parameters and query strings let you get information from the URL.

**Real-World Example:**
Like asking for a specific book in a library by its number (route param) or searching by keyword (query string).

### Route Parameters
- Syntax: `/user/:id`
- Access: `req.params.id`

### Query Strings
- Syntax: `/user?id=123`
- Access: `req.query.id`

### Both Together
```javascript
// /user/123?show=details
app.get('/user/:id', (req, res) => {
  const id = req.params.id;
  const show = req.query.show;
  res.send(`User: ${id}, Show: ${show}`);
});
```

### Practical Examples
- User profile: `/user/42`
- Product detail: `/product/99?ref=homepage`

---

## Organizing Your Express App

**Definition:**
As your app grows, it’s best to split your code into different files and folders.

**Real-World Example:**
Like organizing a big kitchen with separate drawers for spoons, forks, and knives.

### Project Structure
**Flat Structure:**
```
my-express-app/
├── app.js
├── package.json
├── public/
```
**Modular Structure:**
```
my-express-app/
├── app.js
├── routes/
│   └── userRoutes.js
├── controllers/
│   └── userController.js
├── middleware/
│   └── logger.js
├── public/
│   └── index.html
├── .env
└── package.json
```

### Separating Files
- **routes/** for route handlers
- **controllers/** for business logic
- **middleware/** for extra features
- **app.js** for server setup

### Using express.Router()
```javascript
// routes/userRoutes.js
const express = require('express');
const router = express.Router();
const userController = require('../controllers/userController');

router.get('/', userController.getAllUsers);
router.get('/:id', userController.getUserById);
module.exports = router;

// app.js
const userRoutes = require('./routes/userRoutes');
app.use('/users', userRoutes);
```

### Best Practices
- Use clear folder and file names
- Keep business logic out of route files
- Use environment variables for settings (with dotenv)

### Environment Variables with dotenv
```bash
npm install dotenv
```
```javascript
// .env
PORT=4000

// app.js
require('dotenv').config();
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Server on ${PORT}`));
```

---

## Summary

### What We Learned:
- **Express.js** is a simple tool for building web servers
- **Routing** lets you handle different web addresses
- **Middleware** adds features to your app
- **Static files** are easy to serve
- **Route parameters and query strings** help you get info from URLs
- **Good organization** keeps your app easy to manage

### Key Analogies:
- **Express.js** = Food truck kit
- **Routing** = Receptionist
- **Middleware** = Security guard
- **Static files** = Brochure rack
- **Route parameters/query** = Book number and search keyword

---

## Practice Questions

1. What is Express.js and why is it useful?
2. How do you install and set up a basic Express.js app?
3. What is routing in Express?
4. How do you get data from the URL in Express?
5. What is middleware? Give an example.
6. How do you serve static files in Express?
7. Why is it good to organize your code into folders?
8. Write a route that returns a list of products in JSON format.
9. How do you use environment variables in Express?
10. Give a real-world analogy for middleware in Express.js. 

**Ready for Chapter 5? REST API Development for Beginners: Node.js & Express.js!** 

# Chapter 5: REST API Development with Express.js

## Table of Contents
- [What is REST and RESTful APIs?](#what-is-rest-and-restful-apis)
- [Building CRUD APIs using Express.js](#building-crud-apis-using-expressjs)
- [REST API Status Codes and Responses](#rest-api-status-codes-and-responses)
- [Postman Walkthrough for Testing APIs](#postman-walkthrough-for-testing-apis)
- [Creating Custom Middleware (e.g., Logger)](#creating-custom-middleware-eg-logger)
- [Validation using express-validator or Custom Checks](#validation-using-express-validator-or-custom-checks)
- [Handling Errors Globally (Error-handling Middleware)](#handling-errors-globally-error-handling-middleware)
- [Practice Questions](#practice-questions)

---

## What is REST and RESTful APIs?

**Definition:**
REST (Representational State Transfer) is an architectural style for designing networked applications. RESTful APIs use HTTP methods to perform operations on resources, represented as URLs.

**Real-World Example:**
Think of a REST API like a waiter in a restaurant. You (the client) make requests (order food), the waiter (API) brings you what you asked for (data), and you interact using a standard menu (HTTP methods).

**Key Principles:**
- **Stateless:** Each request contains all the information needed
- **Resource-based:** Everything is a resource (user, product, etc.)
- **Standard HTTP methods:** GET, POST, PUT, DELETE
- **Structured URLs:** `/api/books/1`, `/api/users`

**Analogy:**
REST is like a library system: you can search for books (GET), add new books (POST), update book info (PUT), or remove books (DELETE).

---

## Building CRUD APIs using Express.js

**Definition:**
Express.js is a minimal and flexible Node.js web application framework for building APIs and web servers.

**CRUD Operations:**
- **Create:** POST `/api/items`
- **Read:** GET `/api/items` or `/api/items/:id`
- **Update:** PUT `/api/items/:id`
- **Delete:** DELETE `/api/items/:id`

**Example Code:**
```javascript
const express = require('express');
const app = express();
app.use(express.json());

let items = [
  { id: 1, name: 'Item One' },
  { id: 2, name: 'Item Two' }
];

// Create
app.post('/api/items', (req, res) => {
  const { name } = req.body;
  const newItem = { id: items.length + 1, name };
  items.push(newItem);
  res.status(201).json(newItem);
});

// Read all
app.get('/api/items', (req, res) => {
  res.json(items);
});

// Read one
app.get('/api/items/:id', (req, res) => {
  const item = items.find(i => i.id === parseInt(req.params.id));
  if (!item) return res.status(404).json({ error: 'Item not found' });
  res.json(item);
});

// Update
app.put('/api/items/:id', (req, res) => {
  const item = items.find(i => i.id === parseInt(req.params.id));
  if (!item) return res.status(404).json({ error: 'Item not found' });
  item.name = req.body.name;
  res.json(item);
});

// Delete
app.delete('/api/items/:id', (req, res) => {
  const index = items.findIndex(i => i.id === parseInt(req.params.id));
  if (index === -1) return res.status(404).json({ error: 'Item not found' });
  items.splice(index, 1);
  res.json({ message: 'Item deleted' });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

---

## REST API Status Codes and Responses

**Definition:**
Status codes are standard HTTP codes that indicate the result of an API request.

**Common Status Codes:**
- **200 OK:** Request succeeded
- **201 Created:** Resource created
- **400 Bad Request:** Invalid input
- **404 Not Found:** Resource not found
- **500 Internal Server Error:** Server error

**Example:**
```javascript
res.status(201).json({ message: 'Resource created' });
res.status(404).json({ error: 'Not found' });
```

**Analogy:**
Status codes are like traffic lights: green (200) means go, yellow (400) means caution, red (500) means stop!

---

## Postman Walkthrough for Testing APIs

**Definition:**
Postman is a popular tool for testing and documenting APIs.

**How to Use Postman:**
1. **Install Postman** from [postman.com](https://www.postman.com/)
2. **Create a new request** (GET, POST, PUT, DELETE)
3. **Set the URL** (e.g., `http://localhost:3000/api/items`)
4. **Add request body** for POST/PUT (JSON)
5. **Send the request** and view the response

**Real-World Example:**
Postman is like a remote control for your API—you can test every button (endpoint) and see what happens.

---

## Creating Custom Middleware (e.g., Logger)

**Definition:**
Middleware functions in Express.js run during the request-response cycle and can modify requests, responses, or perform actions like logging.

**Logger Middleware Example:**
```javascript
// logger.js
module.exports = (req, res, next) => {
  console.log(`${req.method} ${req.url} at ${new Date().toISOString()}`);
  next();
};

// In app.js
const logger = require('./logger');
app.use(logger);
```

**Analogy:**
Middleware is like a security checkpoint—every request passes through for inspection or logging.

---

## Validation using express-validator or Custom Checks

**Definition:**
Validation ensures incoming data is correct before processing.

**Using express-validator:**
```javascript
const { body, validationResult } = require('express-validator');

app.post('/api/items',
  body('name').notEmpty().withMessage('Name is required'),
  (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    // ... create item
  }
);
```

**Custom Validation Example:**
```javascript
app.post('/api/items', (req, res) => {
  if (!req.body.name) {
    return res.status(400).json({ error: 'Name is required' });
  }
  // ... create item
});
```

---

## Handling Errors Globally (Error-handling Middleware)

**Definition:**
Global error-handling middleware catches and handles errors in one place.

**Example:**
```javascript
// Error-handling middleware (should be last)
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});
```

**Best Practices:**
- Always send meaningful error messages
- Never expose sensitive info in errors
- Use next(err) to pass errors to the handler

---

## Practice Questions

1. What is REST and what makes an API RESTful?
2. How do you build a CRUD API with Express.js?
3. List and explain common HTTP status codes used in REST APIs.
4. How do you use Postman to test an API endpoint?
5. Write a custom logger middleware for Express.js.
6. How do you validate incoming data in Express?
7. What is the purpose of global error-handling middleware?
8. How would you handle a missing required field in a POST request?
9. Why is it important to use status codes in API responses?
10. How can you organize your Express app for scalability and maintainability?

---

**Ready for Chapter 6? Let's dive into the  MongoDB with Mongoose!** 

# Chapter 6: MongoDB with Mongoose

## Table of Contents
- [What is MongoDB? How is it different from SQL?](#what-is-mongodb-how-is-it-different-from-sql)
- [Installing MongoDB locally or using MongoDB Atlas](#installing-mongodb-locally-or-using-mongodb-atlas)
- [Basic MongoDB commands (CRUD) using Mongo shell](#basic-mongodb-commands-crud-using-mongo-shell)
- [What is Mongoose? Why use it?](#what-is-mongoose-why-use-it)
- [Mongoose Setup & Connection with Node](#mongoose-setup--connection-with-node)
- [Defining Schemas and Models](#defining-schemas-and-models)
- [CRUD Operations using Mongoose](#crud-operations-using-mongoose)
- [Mongoose validations](#mongoose-validations)
- [Relationships in MongoDB (References & Population)](#relationships-in-mongodb-references--population)
- [Indexes & performance optimization basics](#indexes--performance-optimization-basics)
- [Practice Questions](#practice-questions)

---

## What is MongoDB? How is it different from SQL?

**Definition:**
MongoDB is a popular open-source NoSQL database that stores data in flexible, JSON-like documents. Unlike traditional SQL databases (like MySQL or PostgreSQL), which use tables and rows, MongoDB uses collections and documents.

**Real-World Example:**
Imagine a filing cabinet. In SQL, every file (row) must have the same fields (columns) in the same order. In MongoDB, each file (document) can have different fields, and you can add new types of information at any time.

**Key Differences:**
- **Schema:** SQL databases have a fixed schema; MongoDB is schema-less (flexible structure).
- **Data Format:** SQL uses tables/rows; MongoDB uses collections/documents (JSON-like).
- **Scalability:** MongoDB is designed for horizontal scaling (easy to add more servers).

**Fun Fact:**
MongoDB’s name comes from “humongous,” reflecting its ability to handle huge amounts of data.

---

## Installing MongoDB locally or using MongoDB Atlas

**Definition:**
You can run MongoDB on your own computer (locally) or use a cloud service like MongoDB Atlas.

**Local Installation:**
1. Go to [mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)
2. Download and install MongoDB Community Edition for your OS
3. Start the MongoDB server (usually with `mongod` command)

**MongoDB Atlas (Cloud):**
1. Go to [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free account
3. Set up a new cluster (cloud database)
4. Get your connection string to use in your apps

**Real-World Example:**
Running MongoDB locally is like having a mini-fridge at home. Using Atlas is like renting a fridge in a shared kitchen that’s always online and managed for you.

---

## Basic MongoDB commands (CRUD) using Mongo shell

**Definition:**
CRUD stands for Create, Read, Update, Delete—the four basic operations for managing data.

**Mongo Shell Examples:**
```js
// Create (Insert)
db.users.insertOne({ name: "Alice", age: 25 })

// Read (Find)
db.users.find({ age: { $gt: 20 } })

// Update
db.users.updateOne({ name: "Alice" }, { $set: { age: 26 } })

// Delete
db.users.deleteOne({ name: "Alice" })
```

**Real-World Example:**
Think of a contact list on your phone: adding a contact (Create), searching for a contact (Read), editing a contact (Update), and deleting a contact (Delete).

**Fun Fact:**
MongoDB queries use JavaScript-like syntax, making it easy for JavaScript developers to learn.

---

## What is Mongoose? Why use it?

**Definition:**
Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides a way to define schemas, models, and validation for your data.

**Why use Mongoose?**
- Enforces structure (schemas) on your documents
- Makes data validation easy
- Provides helpful methods for querying and updating data

**Real-World Example:**
Mongoose is like a helpful librarian who makes sure every book (document) in the library (database) is organized and follows certain rules.

---

## Mongoose Setup & Connection with Node

**Definition:**
To use Mongoose, you install it in your Node.js project and connect it to your MongoDB database.

**Setup Steps:**
1. Install Mongoose:
   ```bash
   npm install mongoose
   ```
2. Connect to MongoDB:
   ```js
   const mongoose = require('mongoose');
   mongoose.connect('mongodb://localhost:27017/mydb', { useNewUrlParser: true, useUnifiedTopology: true })
     .then(() => console.log('Connected to MongoDB'))
     .catch(err => console.error('Connection error', err));
   ```

**Real-World Example:**
Connecting Mongoose to MongoDB is like plugging your laptop into Wi-Fi so you can access the internet (database).

---

## Defining Schemas and Models

**Definition:**
A schema defines the structure of your documents. A model is a wrapper for the schema, providing an interface to interact with the database.

**Example:**
```js
const userSchema = new mongoose.Schema({
  name: String,
  age: Number,
  email: { type: String, required: true }
});
const User = mongoose.model('User', userSchema);
```

**Real-World Example:**
A schema is like a blueprint for a house, and a model is the actual house you build and live in.

---

## CRUD Operations using Mongoose

**Definition:**
Mongoose provides methods to Create, Read, Update, and Delete documents in MongoDB.

**Examples:**
```js
// Create
dbUser = new User({ name: 'Bob', age: 30, email: 'bob@example.com' });
dbUser.save();

// Read
User.find({ age: { $gt: 20 } }).then(users => console.log(users));

// Update
User.updateOne({ name: 'Bob' }, { $set: { age: 31 } });

// Delete
User.deleteOne({ name: 'Bob' });
```

**Real-World Example:**
Managing users in a web app: registering (Create), viewing profiles (Read), editing info (Update), deleting accounts (Delete).

---

## Mongoose validations

**Definition:**
Mongoose allows you to define validation rules in your schema to ensure data is correct before saving.

**Example:**
```js
const productSchema = new mongoose.Schema({
  name: { type: String, required: true },
  price: { type: Number, min: 0 }
});
```

**Real-World Example:**
Validation is like a security guard checking that everyone entering a club is on the guest list and meets the age requirement.

**Fun Fact:**
You can create custom validation functions in Mongoose for advanced checks.

---

## Relationships in MongoDB (References & Population)

**Definition:**
Relationships let you connect documents in different collections, similar to foreign keys in SQL.

**Example:**
```js
const postSchema = new mongoose.Schema({
  title: String,
  author: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
});
```

**Population:**
Mongoose can automatically replace the referenced ObjectId with the actual document using the `populate` method.

**Real-World Example:**
A blog post (Post) references its author (User). Population is like looking up the author’s full profile when viewing the post.

---

## Indexes & performance optimization basics

**Definition:**
Indexes are special data structures that improve the speed of data retrieval operations in MongoDB.

**Example:**
```js
userSchema.index({ email: 1 }); // Create an index on the email field
```

**Real-World Example:**
An index is like the index in a book—it helps you quickly find the page you need without reading the whole book.

**Fun Fact:**
MongoDB automatically creates an index on the `_id` field of every document.

---

## Practice Questions

1. What is MongoDB and how does it differ from SQL databases?
2. How can you install MongoDB locally and what is MongoDB Atlas?
3. Write basic CRUD commands for MongoDB using the shell.
4. What is Mongoose and why is it useful in Node.js projects?
5. How do you connect Mongoose to a MongoDB database?
6. What is the difference between a schema and a model in Mongoose?
7. Show an example of a Mongoose schema with validation.
8. How do you perform CRUD operations using Mongoose?
9. What are references and population in MongoDB/Mongoose?
10. Why are indexes important in MongoDB and how do you create one?

---

**Ready for the next chapter 7? Real-life Project Building (Hands-On)!** 

# Chapter 8: Advanced Concepts & Best Practices

## Table of Contents
- [API Security Basics (Helmet, CORS, rate-limiting)](#api-security-basics-helmet-cors-rate-limiting)
- [Authentication (JWT-based auth step-by-step)](#authentication-jwt-based-auth-step-by-step)
- [Hashing passwords with bcrypt](#hashing-passwords-with-bcrypt)
- [Protecting private routes](#protecting-private-routes)
- [Role-based access control (Admin/User)](#role-based-access-control-adminuser)
- [Pagination and filtering](#pagination-and-filtering)
- [Express error handling best practices](#express-error-handling-best-practices)
- [Project structure for scalable apps](#project-structure-for-scalable-apps)
- [Deploying Node.js App (Railway, Render, Vercel, or Heroku)](#deploying-nodejs-app-railway-render-vercel-or-heroku)
- [Git & GitHub basics for deployment (.gitignore, package.json scripts)](#git--github-basics-for-deployment-gitignore-packagejson-scripts)
- [Practice Questions](#practice-questions)

---

## API Security Basics (Helmet, CORS, rate-limiting)

**Definition:**
API security involves protecting your application’s endpoints from unauthorized access, attacks, and misuse.

**Helmet:**
Helmet is a middleware for Express that sets various HTTP headers to help secure your app.
```js
const helmet = require('helmet');
app.use(helmet());
```

**CORS (Cross-Origin Resource Sharing):**
CORS controls which domains can access your API. By default, browsers block requests from different origins for security.
```js
const cors = require('cors');
app.use(cors({ origin: 'https://your-frontend.com' }));
```

**Rate Limiting:**
Rate limiting restricts the number of requests a user can make in a given time frame, protecting against brute-force and denial-of-service attacks.
```js
const rateLimit = require('express-rate-limit');
app.use(rateLimit({ windowMs: 15 * 60 * 1000, max: 100 }));
```

**Real-World Example:**
Think of a security guard (Helmet) checking IDs, a bouncer (CORS) only letting in people from certain companies, and a ticket counter (rate-limiting) only selling a certain number of tickets per hour.

**Fun Fact:**
Helmet can help prevent over 10 common web vulnerabilities with just one line of code.

---

## Authentication (JWT-based auth step-by-step)

**Definition:**
Authentication is the process of verifying a user’s identity. JWT (JSON Web Token) is a compact, URL-safe way to represent claims between two parties.

**Step-by-Step JWT Auth:**
1. User logs in with username and password.
2. Server verifies credentials and creates a JWT.
3. JWT is sent to the client and stored (usually in localStorage or a cookie).
4. Client sends JWT in the Authorization header for protected requests.
5. Server verifies the JWT before allowing access to protected routes.

**Example:**
```js
const jwt = require('jsonwebtoken');
const token = jwt.sign({ userId: user._id }, 'secretKey', { expiresIn: '1h' });
// To verify:
jwt.verify(token, 'secretKey');
```

**Real-World Example:**
JWT is like a movie ticket: once you have it, you can show it to enter the theater (protected route) until it expires.

---

## Hashing passwords with bcrypt

**Definition:**
Hashing is the process of converting a password into a fixed-length string of characters, which is nearly impossible to reverse. bcrypt is a popular library for hashing passwords in Node.js.

**Example:**
```js
const bcrypt = require('bcrypt');
const hashed = await bcrypt.hash('myPassword', 10);
const isMatch = await bcrypt.compare('myPassword', hashed);
```

**Real-World Example:**
Hashing is like shredding a document—once shredded, you can’t put it back together, but you can compare shreds to see if they came from the same document.

**Fun Fact:**
bcrypt automatically adds a random “salt” to each password, making it even more secure.

---

## Protecting private routes

**Definition:**
Private routes are endpoints that require authentication. Only users with valid tokens can access them.

**Example:**
```js
function authMiddleware(req, res, next) {
  const token = req.headers.authorization?.split(' ')[1];
  if (!token) return res.status(401).send('Access denied');
  try {
    const decoded = jwt.verify(token, 'secretKey');
    req.user = decoded;
    next();
  } catch {
    res.status(400).send('Invalid token');
  }
}
app.get('/private', authMiddleware, (req, res) => {
  res.send('This is a private route');
});
```

**Real-World Example:**
A private route is like a VIP lounge—only people with the right wristband (token) can enter.

---

## Role-based access control (Admin/User)

**Definition:**
Role-based access control (RBAC) restricts what users can do based on their assigned roles (e.g., admin, user).

**Example:**
```js
function adminMiddleware(req, res, next) {
  if (req.user.role !== 'admin') return res.status(403).send('Admins only');
  next();
}
app.delete('/admin/delete-user', authMiddleware, adminMiddleware, (req, res) => {
  // delete logic
});
```

**Real-World Example:**
RBAC is like different access cards in an office—some open every door (admin), some only open certain rooms (user).

---

## Pagination and filtering

**Definition:**
Pagination breaks large sets of data into smaller pages. Filtering allows users to search or narrow down results.

**Example:**
```js
// Pagination
const page = parseInt(req.query.page) || 1;
const limit = parseInt(req.query.limit) || 10;
const users = await User.find().skip((page - 1) * limit).limit(limit);

// Filtering
const filtered = await User.find({ age: { $gte: 18 } });
```

**Real-World Example:**
Pagination is like a book’s table of contents—showing a few chapters at a time. Filtering is like searching for all chapters about a specific topic.

---

## Express error handling best practices

**Definition:**
Error handling ensures your app responds gracefully to problems, providing useful feedback without crashing.

**Example:**
```js
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something went wrong!');
});
```

**Best Practices:**
- Use centralized error handling middleware
- Don’t leak sensitive info in error messages
- Log errors for debugging

**Real-World Example:**
Error handling is like a car’s airbag—it protects users when something goes wrong.

---

## Project structure for scalable apps

**Definition:**
A well-organized project structure makes your app easier to maintain and scale.

**Example Structure:**
```
project-root/
  controllers/
  models/
  routes/
  middlewares/
  utils/
  app.js
  package.json
```

**Real-World Example:**
A good project structure is like a well-organized kitchen—everything has its place, making cooking (coding) efficient.

**Fun Fact:**
Many large companies use similar folder structures for their Node.js apps.

---

## Deploying Node.js App (Railway, Render, Vercel, or Heroku)

**Definition:**
Deployment is the process of making your app available on the internet. Platforms like Railway, Render, Vercel, and Heroku make this easy.

**Steps:**
1. Push your code to GitHub
2. Connect your GitHub repo to the deployment platform
3. Configure environment variables (like database URLs)
4. Deploy and monitor your app

**Real-World Example:**
Deploying is like opening your restaurant to the public after setting up the kitchen and menu.

---

## Git & GitHub basics for deployment (.gitignore, package.json scripts)

**Definition:**
Git is a version control system; GitHub is a platform for hosting and collaborating on code.

**.gitignore:**
Specifies files/folders Git should ignore (like node_modules, .env).

**package.json scripts:**
Custom commands for running, building, or deploying your app.
```json
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js"
}
```

**Real-World Example:**
.gitignore is like a do-not-pack list for a trip. package.json scripts are like shortcuts for common tasks.

---

## Practice Questions

1. What does Helmet do in an Express app?
2. How does CORS help secure your API?
3. What is rate limiting and why is it important?
4. Explain the steps of JWT-based authentication.
5. How do you hash and verify passwords with bcrypt?
6. How do you protect private routes in Express?
7. What is role-based access control and how is it implemented?
8. Show an example of pagination and filtering in a Node.js API.
9. What are best practices for error handling in Express?
10. Describe a scalable project structure for a Node.js app.
11. What are the steps to deploy a Node.js app to a cloud platform?
12. What is the purpose of .gitignore and package.json scripts?

---

