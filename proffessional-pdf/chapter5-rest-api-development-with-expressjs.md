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