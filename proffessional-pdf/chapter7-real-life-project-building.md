# Chapter 7: Real-life Project Building (Hands-On)

## Table of Contents
- [Project Overview](#project-overview)
- [Setting Up the Project](#setting-up-the-project)
- [MVC Folder Structure](#mvc-folder-structure)
- [Using .env Files and dotenv Package](#using-env-files-and-dotenv-package)
- [Connecting to MongoDB Atlas](#connecting-to-mongodb-atlas)
- [CRUD Operations](#crud-operations)
  - [Add Operation](#add-operation)
  - [Get Operation](#get-operation)
  - [Update Operation](#update-operation)
  - [Delete Operation](#delete-operation)
- [Field Validation Before Saving](#field-validation-before-saving)
- [Error Handling and Custom Messages](#error-handling-and-custom-messages)
- [Logger Middleware (Morgan or Custom)](#logger-middleware-morgan-or-custom)
- [Practice Questions](#practice-questions)

---

## Project Overview

**Goal:** Build a real-life Node.js REST API project with full CRUD (Create, Read, Update, Delete) operations, using MongoDB Atlas for cloud storage, robust validation, error handling, and best practices like MVC structure and environment variables.

**Real-World Example:**
Imagine building a digital library system where users can add, update, delete, and view books. All data is stored securely in the cloud (MongoDB Atlas), and the system is organized for easy maintenance and scalability.

---

## Setting Up the Project

1. **Initialize Node.js project:**
   ```bash
   npm init -y
   ```
2. **Install dependencies:**
   ```bash
   npm install express mongoose dotenv morgan
   ```
3. **Create folder structure:**
   - `controllers/`
   - `models/`
   - `routes/`
   - `middlewares/`
   - `config/`
   - `app.js`
   - `.env`

---

## MVC Folder Structure

**Definition:**
MVC (Model-View-Controller) is a design pattern that separates application logic (controllers), data (models), and routing (routes).

**Analogy:**
Think of MVC like a restaurant:
- **Model:** The kitchen (where data/food is prepared)
- **Controller:** The waiter (handles requests and delivers responses)
- **Route:** The menu (decides which request goes where)

**Example Structure:**
```
project/
  controllers/
    bookController.js
  models/
    book.js
  routes/
    bookRoutes.js
  middlewares/
    logger.js
  config/
    db.js
  app.js
  .env
```

---

## Using .env Files and dotenv Package

**Definition:**
`.env` files store sensitive configuration (like database URIs) outside your code. The `dotenv` package loads these variables into `process.env`.

**Real-World Example:**
Like keeping your house keys in a safe instead of leaving them on the front door.

**.env Example:**
```
MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/mydb
PORT=3000
```

**Usage in Code:**
```javascript
require('dotenv').config();
const port = process.env.PORT || 3000;
const dbUri = process.env.MONGODB_URI;
```

---

## Connecting to MongoDB Atlas

**Definition:**
MongoDB Atlas is a cloud database service. Use Mongoose to connect and interact with it.

**Code Example:**
```javascript
// config/db.js
const mongoose = require('mongoose');

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGODB_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    console.log('MongoDB connected!');
  } catch (err) {
    console.error('MongoDB connection error:', err.message);
    process.exit(1);
  }
};

module.exports = connectDB;
```

**In app.js:**
```javascript
const connectDB = require('./config/db');
connectDB();
```

---

## CRUD Operations

### Add Operation
**Definition:** Create a new record in the database.

**Code Example:**
```javascript
// controllers/bookController.js
const Book = require('../models/book');

exports.addBook = async (req, res) => {
  try {
    const { title, author, year } = req.body;
    const book = new Book({ title, author, year });
    await book.save();
    res.status(201).json({ message: 'Book added!', book });
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
};
```

### Get Operation
**Definition:** Retrieve records from the database.

**Code Example:**
```javascript
exports.getBooks = async (req, res) => {
  try {
    const books = await Book.find();
    res.json(books);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
};
```

### Update Operation
**Definition:** Modify an existing record.

**Code Example:**
```javascript
exports.updateBook = async (req, res) => {
  try {
    const { id } = req.params;
    const { title, author, year } = req.body;
    const book = await Book.findByIdAndUpdate(
      id,
      { title, author, year },
      { new: true, runValidators: true }
    );
    if (!book) return res.status(404).json({ error: 'Book not found' });
    res.json({ message: 'Book updated!', book });
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
};
```

### Delete Operation
**Definition:** Remove a record from the database.

**Code Example:**
```javascript
exports.deleteBook = async (req, res) => {
  try {
    const { id } = req.params;
    const book = await Book.findByIdAndDelete(id);
    if (!book) return res.status(404).json({ error: 'Book not found' });
    res.json({ message: 'Book deleted!' });
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
};
```

---

## Field Validation Before Saving

**Definition:** Ensure all required fields are present and valid before saving to the database.

**Mongoose Schema Example:**
```javascript
// models/book.js
const mongoose = require('mongoose');

const bookSchema = new mongoose.Schema({
  title: { type: String, required: [true, 'Title is required'] },
  author: { type: String, required: [true, 'Author is required'] },
  year: { type: Number, min: [1000, 'Year must be after 1000'] },
});

module.exports = mongoose.model('Book', bookSchema);
```

**Custom Validation Example:**
```javascript
if (!title || !author) {
  return res.status(400).json({ error: 'Title and author are required' });
}
```

---

## Error Handling and Custom Messages

**Definition:** Provide clear, user-friendly error messages and handle exceptions gracefully.

**Example:**
```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});
```

**Custom Error Messages:**
- Book not found
- Validation failed: Title is required
- Database connection error

---

## Logger Middleware (Morgan or Custom)

**Definition:** Middleware that logs HTTP requests for debugging and monitoring.

**Using Morgan:**
```javascript
const morgan = require('morgan');
app.use(morgan('dev'));
```

**Custom Logger Example:**
```javascript
// middlewares/logger.js
module.exports = (req, res, next) => {
  console.log(`${req.method} ${req.url} at ${new Date().toISOString()}`);
  next();
};

// In app.js
const logger = require('./middlewares/logger');
app.use(logger);
```

---

## Practice Questions

1. What is the MVC pattern and why is it useful?
2. How do you connect a Node.js app to MongoDB Atlas?
3. Write code to add a new book with validation.
4. How do you handle errors and send custom messages in Express?
5. What is the purpose of .env files?
6. How would you implement a logger middleware?
7. What are the benefits of using Mongoose for MongoDB?
8. How do you update a record and ensure validation?
9. What happens if you try to delete a non-existent record?
10. How would you organize your project for scalability?

---

**Ready for the next challenge? Try building your own REST API with different resources and advanced features!** 
