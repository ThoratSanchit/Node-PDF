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