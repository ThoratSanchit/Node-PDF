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

