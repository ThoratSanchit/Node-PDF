# MySQL Database Complete Guide

## Index

- [Chapter 1: Introduction to MySQL Database](#chapter-1-introduction-to-mysql-database)
- [Chapter 2: MySQL Installation and Setup](#chapter-2-mysql-installation-and-setup)
- [Chapter 3: Basic SQL Commands and Queries](#chapter-3-basic-sql-commands-and-queries)
- [Chapter 4: Database Design and Normalization](#chapter-4-database-design-and-normalization)
- [Chapter 5: Advanced SQL Queries and Joins](#chapter-5-advanced-sql-queries-and-joins)
- [Chapter 6: MySQL with Node.js and Express](#chapter-6-mysql-with-nodejs-and-express)
- [Chapter 7: Real-Life Project: E-commerce Database](#chapter-7-real-life-project-e-commerce-database)
- [Chapter 8: Advanced MySQL Concepts and Best Practices](#chapter-8-advanced-mysql-concepts-and-best-practices)

---

# Chapter 1: Introduction to MySQL Database

## Table of Contents
- [What is MySQL?](#what-is-mysql)
- [Why use MySQL?](#why-use-mysql)
- [MySQL vs Other Databases](#mysql-vs-other-databases)
- [Understanding Relational Databases](#understanding-relational-databases)
- [MySQL Architecture](#mysql-architecture)
- [Common Use Cases](#common-use-cases)

---

## What is MySQL?

**Definition:**
MySQL is an open-source relational database management system (RDBMS) that uses Structured Query Language (SQL) to store, organize, and retrieve data efficiently.

**Real-World Example:**
Think of MySQL like a digital filing cabinet with multiple drawers (tables). Each drawer contains related information (like customer records, product inventory, or order history), and you can quickly find any piece of information using specific instructions (SQL queries).

**Fun Fact:**
MySQL was created in 1995 by Michael Widenius and is now owned by Oracle Corporation. It's used by major companies like Facebook, Twitter, and YouTube.

### Key Points:
- **Relational:** Data is organized in tables with relationships between them
- **SQL-based:** Uses standard SQL language for data operations
- **Open-source:** Free to use and modify
- **Cross-platform:** Works on Windows, Mac, Linux, and more

> **Analogy:** MySQL is like a super-organized library where every book (data) has a specific location, and the librarian (SQL) can find any book instantly.

---

## Why use MySQL?

**Definition:**
MySQL is chosen for its reliability, performance, ease of use, and wide community support.

### 1. Reliability and Performance

**Definition:**
MySQL is known for its stability and fast performance, even with large amounts of data.

**Real-World Example:**
Like a well-oiled machine that can handle thousands of customers at a busy restaurant without slowing down.

**What this means:** MySQL can process millions of records quickly and reliably.

### 2. Ease of Use

**Definition:**
MySQL is designed to be user-friendly, with clear syntax and helpful error messages.

**Real-World Example:**
Like learning to drive an automatic car instead of a manual transmission - it's easier to get started.

```sql
-- Simple query to get all users
SELECT * FROM users;

-- Simple query to add a new user
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');
```

### 3. Cost-Effective

**Definition:**
MySQL is free to use and doesn't require expensive licenses.

**Real-World Example:**
Like getting a high-quality tool for free instead of paying thousands of dollars for similar functionality.

### 4. Large Community

**Definition:**
MySQL has millions of users worldwide, providing extensive documentation and support.

**Real-World Example:**
Like having access to a huge community of experts who can help you solve any problem.

---

## MySQL vs Other Databases

**Definition:**
Different databases serve different purposes. Understanding the differences helps you choose the right tool for your project.

### MySQL vs PostgreSQL

| Feature | MySQL | PostgreSQL |
|---------|-------|------------|
| **Performance** | Fast for read-heavy workloads | Excellent for complex queries |
| **Features** | Simple and straightforward | Advanced features (JSON, arrays) |
| **Learning Curve** | Easier to learn | More complex but powerful |
| **Use Case** | Web applications, e-commerce | Complex applications, data analysis |

### MySQL vs MongoDB (NoSQL)

| Feature | MySQL | MongoDB |
|---------|-------|---------|
| **Data Structure** | Tables with rows and columns | Documents (JSON-like) |
| **Schema** | Fixed schema required | Flexible schema |
| **Relationships** | Foreign keys and joins | Embedded documents or references |
| **Use Case** | Structured data, transactions | Unstructured data, rapid development |

**Real-World Example:**
- **MySQL:** Like a spreadsheet with strict rules
- **MongoDB:** Like a flexible notebook where you can write anything anywhere

---

## Understanding Relational Databases

**Definition:**
A relational database organizes data into tables (relations) that can be linked together using relationships.

### Tables and Relationships

**Definition:**
Tables are like spreadsheets with rows (records) and columns (fields). Relationships connect data between tables.

**Real-World Example:**
Think of a school database:
- **Students table:** Student ID, Name, Grade
- **Classes table:** Class ID, Subject, Teacher
- **Enrollments table:** Student ID, Class ID (connects students to classes)

```sql
-- Students table
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    grade INT
);

-- Classes table
CREATE TABLE classes (
    class_id INT PRIMARY KEY,
    subject VARCHAR(50),
    teacher VARCHAR(100)
);

-- Enrollments table (relationship table)
CREATE TABLE enrollments (
    student_id INT,
    class_id INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (class_id) REFERENCES classes(class_id)
);
```

### Types of Relationships

1. **One-to-One:** One record in Table A relates to one record in Table B
   - Example: User and UserProfile (one user has one profile)

2. **One-to-Many:** One record in Table A relates to many records in Table B
   - Example: Customer and Orders (one customer can have many orders)

3. **Many-to-Many:** Many records in Table A relate to many records in Table B
   - Example: Students and Classes (many students can take many classes)

---

## MySQL Architecture

**Definition:**
MySQL's architecture consists of several components that work together to manage data efficiently.

### Core Components

```
┌─────────────────────────────────────┐
│           Client Applications       │
├─────────────────────────────────────┤
│           MySQL Server              │
│  ┌─────────────┐ ┌─────────────┐   │
│  │ Connection  │ │ Query Cache │   │
│  │  Manager    │ │             │   │
│  └─────────────┘ └─────────────┘   │
│  ┌─────────────┐ ┌─────────────┐   │
│  │ Parser &    │ │ Optimizer   │   │
│  │ Analyzer    │ │             │   │
│  └─────────────┘ └─────────────┘   │
│  ┌─────────────┐ ┌─────────────┐   │
│  │ Storage     │ │ Buffer Pool │   │
│  │ Engine      │ │             │   │
│  └─────────────┘ └─────────────┘   │
├─────────────────────────────────────┤
│           Data Files                │
└─────────────────────────────────────┘
```

**Analogy:**
- **Connection Manager:** Like a receptionist who directs visitors
- **Query Cache:** Like a memory bank for frequently asked questions
- **Parser & Analyzer:** Like a translator who understands your request
- **Optimizer:** Like a smart planner who finds the best route
- **Storage Engine:** Like a warehouse where data is stored
- **Buffer Pool:** Like a temporary storage area for quick access

### Storage Engines

**Definition:**
Storage engines determine how data is stored, indexed, and retrieved.

**Common Engines:**
- **InnoDB:** Default engine, supports transactions and foreign keys
- **MyISAM:** Faster for read-heavy workloads, no transaction support
- **Memory:** Stores data in RAM for ultra-fast access

---

## Common Use Cases

**Definition:**
MySQL is used in various applications across different industries.

### 1. Web Applications

**Real-World Example:**
Most websites use MySQL to store user accounts, content, and application data.

```sql
-- Example: User management system
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) UNIQUE,
    email VARCHAR(100) UNIQUE,
    password_hash VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2. E-commerce Platforms

**Real-World Example:**
Online stores use MySQL for product catalogs, customer orders, and inventory management.

```sql
-- Example: Product catalog
CREATE TABLE products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(200),
    description TEXT,
    price DECIMAL(10,2),
    stock_quantity INT,
    category_id INT,
    FOREIGN KEY (category_id) REFERENCES categories(category_id)
);
```

### 3. Content Management Systems

**Real-World Example:**
Blogs and websites use MySQL to store articles, comments, and user-generated content.

### 4. Business Applications

**Real-World Example:**
Companies use MySQL for customer relationship management (CRM), inventory tracking, and financial records.

---

## Summary

### What We Learned:
- **MySQL** is a powerful, open-source relational database
- **Relational databases** organize data in tables with relationships
- **MySQL architecture** consists of multiple components working together
- **Common use cases** include web apps, e-commerce, and business systems
- **MySQL vs other databases** - each has strengths for different scenarios

### Key Analogies:
- **MySQL** = Digital filing cabinet
- **Tables** = Drawers in the filing cabinet
- **Relationships** = Connections between different drawers
- **SQL** = Instructions for the filing system
- **Storage Engine** = Type of filing system used

### Next Steps:
In the next chapter, we'll learn how to **install and set up MySQL** on your computer!

---

## Practice Questions

1. What is MySQL and what makes it different from other databases?
2. Explain the concept of relational databases with a real-world example.
3. What are the three types of relationships in databases? Give examples of each.
4. Why is MySQL considered cost-effective for businesses?
5. Compare MySQL with MongoDB - when would you use each?
6. What are the main components of MySQL architecture?
7. Give three common use cases for MySQL in real-world applications.
8. What is a storage engine in MySQL and name two common ones?
9. Explain the analogy of MySQL being like a digital filing cabinet.
10. What are the advantages of MySQL's large community support?

---

**Ready for Chapter 2? Let's learn how to install and set up MySQL!**

# Chapter 2: MySQL Installation and Setup

## Table of Contents
- [Installing MySQL on Different Operating Systems](#installing-mysql-on-different-operating-systems)
- [MySQL Workbench Installation](#mysql-workbench-installation)
- [First Connection to MySQL Server](#first-connection-to-mysql-server)
- [Understanding MySQL Users and Privileges](#understanding-mysql-users-and-privileges)
- [Creating Your First Database](#creating-your-first-database)
- [Basic MySQL Configuration](#basic-mysql-configuration)
- [Troubleshooting Common Installation Issues](#troubleshooting-common-installation-issues)

---

## Installing MySQL on Different Operating Systems

**Definition:**
MySQL can be installed on various operating systems. The installation process differs slightly for each platform.

### Windows Installation

**Step-by-Step Process:**

1. **Download MySQL Installer:**
   - Go to [mysql.com/downloads/installer](https://dev.mysql.com/downloads/installer/)
   - Download "MySQL Installer for Windows"

2. **Run the Installer:**
   ```bash
   # Double-click the downloaded .msi file
   # Choose "Developer Default" for full installation
   ```

3. **Configure MySQL Server:**
   - Set root password (remember this!)
   - Choose port (default: 3306)
   - Configure Windows service

**Real-World Example:**
Like installing a new app on your phone - you download it, run the installer, and follow the setup wizard.

### macOS Installation

**Option 1: Using Homebrew (Recommended):**
```bash
# Install Homebrew first (if not installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install MySQL
brew install mysql

# Start MySQL service
brew services start mysql

# Secure the installation
mysql_secure_installation
```

**Option 2: Using DMG Installer:**
- Download MySQL DMG from mysql.com
- Install like any other macOS application

### Linux Installation (Ubuntu/Debian)

**Using Package Manager:**
```bash
# Update package list
sudo apt update

# Install MySQL
sudo apt install mysql-server

# Start MySQL service
sudo systemctl start mysql

# Secure the installation
sudo mysql_secure_installation
```

**Real-World Example:**
Like setting up a new appliance in your kitchen - you need to install it, plug it in, and configure the settings.

---

## MySQL Workbench Installation

**Definition:**
MySQL Workbench is a visual tool for designing, developing, and administering MySQL databases.

### Why Use MySQL Workbench?

**Benefits:**
- **Visual Interface:** No need to remember SQL commands
- **Database Design:** Create ER diagrams visually
- **Query Editor:** Write and test SQL queries
- **Server Administration:** Manage users, backups, and monitoring

**Real-World Example:**
Like having a remote control for your TV instead of manually adjusting settings on the back panel.

### Installation Steps

1. **Download MySQL Workbench:**
   - Go to [mysql.com/products/workbench](https://dev.mysql.com/downloads/workbench/)
   - Download for your operating system

2. **Install and Launch:**
   ```bash
   # Windows: Run the .msi installer
   # macOS: Install the .dmg file
   # Linux: sudo apt install mysql-workbench
   ```

3. **Connect to MySQL Server:**
   - Open MySQL Workbench
   - Click "Database" → "Connect to Database"
   - Enter connection details

---

## First Connection to MySQL Server

**Definition:**
After installation, you need to connect to the MySQL server to start working with databases.

### Using Command Line

**Windows:**
```bash
# Open Command Prompt and navigate to MySQL bin directory
cd "C:\Program Files\MySQL\MySQL Server 8.0\bin"

# Connect to MySQL
mysql -u root -p
# Enter your password when prompted
```

**macOS/Linux:**
```bash
# Connect to MySQL
mysql -u root -p
# Enter your password when prompted
```

### Using MySQL Workbench

1. **Open MySQL Workbench**
2. **Click "Database" → "Connect to Database"**
3. **Enter connection details:**
   - Hostname: localhost
   - Port: 3306
   - Username: root
   - Password: (your root password)

### Successful Connection

**What you should see:**
```sql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.33 MySQL Community Server (GPL)

mysql>
```

**Real-World Example:**
Like successfully logging into your email account - you see a welcome message and can start using the system.

---

## Understanding MySQL Users and Privileges

**Definition:**
MySQL uses a user-based security system where different users have different levels of access to databases and tables.

### Default Users

**Root User:**
- **Purpose:** Superuser with all privileges
- **Use:** Administration tasks only
- **Security:** Should not be used for applications

**Real-World Example:**
Root is like the master key to a building - it opens everything but should be used carefully.

### Creating New Users

**Basic User Creation:**
```sql
-- Create a new user
CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';

-- Grant privileges to the user
GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';

-- Apply the changes
FLUSH PRIVILEGES;
```

**User with Limited Privileges:**
```sql
-- Create user for specific database
CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'apppassword';

-- Grant only SELECT and INSERT privileges
GRANT SELECT, INSERT ON mydatabase.* TO 'appuser'@'localhost';

FLUSH PRIVILEGES;
```

### Understanding Privileges

**Common Privileges:**
- **SELECT:** Read data from tables
- **INSERT:** Add new data to tables
- **UPDATE:** Modify existing data
- **DELETE:** Remove data from tables
- **CREATE:** Create new databases/tables
- **DROP:** Delete databases/tables
- **ALL PRIVILEGES:** Full access

**Real-World Example:**
Privileges are like different levels of access cards in an office building - some people can only enter certain rooms, others can access everything.

---

## Creating Your First Database

**Definition:**
A database is a container that holds related tables and data.

### Creating a Database

**Basic Database Creation:**
```sql
-- Create a new database
CREATE DATABASE my_first_database;

-- Show all databases
SHOW DATABASES;

-- Use the database
USE my_first_database;
```

### Creating Your First Table

**Simple Table Example:**
```sql
-- Create a users table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Show tables in the database
SHOW TABLES;

-- Describe the table structure
DESCRIBE users;
```

### Adding Data to Your Table

**Inserting Records:**
```sql
-- Insert a single user
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');

-- Insert multiple users
INSERT INTO users (name, email) VALUES 
    ('Jane Smith', 'jane@example.com'),
    ('Bob Johnson', 'bob@example.com');

-- View all users
SELECT * FROM users;
```

**Real-World Example:**
Like creating a new folder on your computer, then adding files to it. The folder is the database, and the files are the tables.

---

## Basic MySQL Configuration

**Definition:**
MySQL configuration involves setting up the server for optimal performance and security.

### Configuration File Location

**Windows:**
```
C:\ProgramData\MySQL\MySQL Server 8.0\my.ini
```

**macOS:**
```
/usr/local/etc/my.cnf
```

**Linux:**
```
/etc/mysql/my.cnf
```

### Important Configuration Settings

**Basic Settings:**
```ini
[mysqld]
# Port number
port = 3306

# Maximum connections
max_connections = 151

# Buffer pool size (for InnoDB)
innodb_buffer_pool_size = 128M

# Query cache size
query_cache_size = 16M

# Character set
character-set-server = utf8mb4
```

**Real-World Example:**
Like adjusting the settings on your car - you can change the seat position, mirror angles, and radio stations to suit your preferences.

### Security Configuration

**Essential Security Steps:**
```sql
-- Remove anonymous users
DELETE FROM mysql.user WHERE User='';

-- Remove test database
DROP DATABASE IF EXISTS test;

-- Reload privileges
FLUSH PRIVILEGES;
```

---

## Troubleshooting Common Installation Issues

**Definition:**
Common problems that occur during MySQL installation and how to solve them.

### Common Issues and Solutions

**1. "Access Denied" Error:**
```bash
# Problem: Can't connect to MySQL
# Solution: Reset root password
sudo mysqld_safe --skip-grant-tables &
mysql -u root
UPDATE mysql.user SET authentication_string=PASSWORD('newpassword') WHERE User='root';
FLUSH PRIVILEGES;
```

**2. "Port Already in Use" Error:**
```bash
# Problem: Port 3306 is already used
# Solution: Find and stop the process
# Windows:
netstat -ano | findstr :3306
taskkill /PID <process_id> /F

# Linux/macOS:
sudo lsof -i :3306
sudo kill -9 <process_id>
```

**3. "Service Won't Start" Error:**
```bash
# Problem: MySQL service fails to start
# Solution: Check error logs
# Windows: Check Event Viewer
# Linux/macOS: Check /var/log/mysql/error.log
```

**Real-World Example:**
Like troubleshooting a car that won't start - you check the battery, fuel, and engine to find the problem.

---

## Summary

### What We Learned:
- **MySQL installation** varies by operating system
- **MySQL Workbench** provides a visual interface for database management
- **User management** is crucial for security
- **Database creation** is the first step in working with MySQL
- **Configuration** optimizes performance and security
- **Troubleshooting** helps solve common installation problems

### Key Analogies:
- **MySQL Installation** = Setting up a new appliance
- **MySQL Workbench** = Remote control for your database
- **Users and Privileges** = Access cards with different permissions
- **Database Creation** = Creating a new folder for organizing files
- **Configuration** = Adjusting car settings for optimal performance

### Next Steps:
In the next chapter, we'll learn **basic SQL commands and queries** to work with your database!

---

## Practice Questions

1. What are the different ways to install MySQL on Windows, macOS, and Linux?
2. Why is MySQL Workbench useful for database management?
3. How do you connect to MySQL server for the first time?
4. What is the difference between the root user and regular users in MySQL?
5. How do you create a new database and table in MySQL?
6. What are MySQL privileges and why are they important?
7. Where are MySQL configuration files located on different operating systems?
8. How do you troubleshoot a "port already in use" error?
9. What security steps should you take after installing MySQL?
10. Explain the analogy of MySQL users being like access cards in an office building.

---

**Ready for Chapter 3? Let's learn basic SQL commands and queries!**

# Chapter 3: Basic SQL Commands and Queries

## Table of Contents
- [Understanding SQL Syntax](#understanding-sql-syntax)
- [SELECT Statement - Reading Data](#select-statement---reading-data)
- [INSERT Statement - Adding Data](#insert-statement---adding-data)
- [UPDATE Statement - Modifying Data](#update-statement---modifying-data)
- [DELETE Statement - Removing Data](#delete-statement---removing-data)
- [WHERE Clause - Filtering Data](#where-clause---filtering-data)
- [ORDER BY - Sorting Results](#order-by---sorting-results)
- [LIMIT and OFFSET - Controlling Results](#limit-and-offset---controlling-results)
- [Working with NULL Values](#working-with-null-values)
- [Data Types in MySQL](#data-types-in-mysql)

---

## Understanding SQL Syntax

**Definition:**
SQL (Structured Query Language) is the standard language for interacting with relational databases. It has specific syntax rules and conventions.

### Basic SQL Rules

**Key Syntax Rules:**
- **Statements end with semicolon (;)**
- **Keywords are not case-sensitive** (SELECT = select = Select)
- **String values must be in quotes** ('text' or "text")
- **Numbers don't need quotes** (123, 45.67)

**Real-World Example:**
Like learning the grammar rules of a new language - you need to follow the correct structure to be understood.

### SQL Statement Structure

**Basic Pattern:**
```sql
SELECT column1, column2
FROM table_name
WHERE condition
ORDER BY column1;
```

**Analogy:**
Think of SQL like giving instructions to a librarian:
- **SELECT:** What information you want
- **FROM:** Which book (table) to look in
- **WHERE:** What criteria to match
- **ORDER BY:** How to organize the results

---

## SELECT Statement - Reading Data

**Definition:**
The SELECT statement retrieves data from one or more tables in the database.

### Basic SELECT Syntax

**Selecting All Columns:**
```sql
-- Get all data from users table
SELECT * FROM users;

-- Get specific columns
SELECT name, email FROM users;
```

**Real-World Example:**
Like asking a librarian to show you all books in a section, or just the titles and authors.

### Selecting Specific Columns

**Column Selection Examples:**
```sql
-- Select single column
SELECT name FROM users;

-- Select multiple columns
SELECT id, name, email FROM users;

-- Use aliases for column names
SELECT name AS user_name, email AS user_email FROM users;
```

**Benefits of Selecting Specific Columns:**
- **Performance:** Faster queries
- **Clarity:** Only relevant data
- **Security:** Avoid exposing sensitive data

---

## INSERT Statement - Adding Data

**Definition:**
The INSERT statement adds new records (rows) to a table.

### Basic INSERT Syntax

**Inserting Single Record:**
```sql
-- Insert one user
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');

-- Insert with all columns (if you know the order)
INSERT INTO users VALUES (NULL, 'Jane Smith', 'jane@example.com', NOW());
```

**Inserting Multiple Records:**
```sql
-- Insert multiple users at once
INSERT INTO users (name, email) VALUES 
    ('Alice Johnson', 'alice@example.com'),
    ('Bob Wilson', 'bob@example.com'),
    ('Carol Brown', 'carol@example.com');
```

**Real-World Example:**
Like adding new contact cards to your address book - you fill in the information and add it to the collection.

### INSERT with Different Scenarios

**Handling Auto-increment IDs:**
```sql
-- Let MySQL generate the ID automatically
INSERT INTO users (name, email) VALUES ('New User', 'new@example.com');

-- Check what ID was assigned
SELECT LAST_INSERT_ID();
```

**Inserting with Default Values:**
```sql
-- Create table with default values
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) DEFAULT 0.00,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Insert with defaults
INSERT INTO products (name) VALUES ('Sample Product');
```

---

## UPDATE Statement - Modifying Data

**Definition:**
The UPDATE statement modifies existing records in a table.

### Basic UPDATE Syntax

**Updating Single Record:**
```sql
-- Update user's email
UPDATE users SET email = 'newemail@example.com' WHERE id = 1;

-- Update multiple columns
UPDATE users SET name = 'John Smith', email = 'johnsmith@example.com' WHERE id = 1;
```

**Updating Multiple Records:**
```sql
-- Update all users with a specific condition
UPDATE users SET status = 'active' WHERE created_at < '2023-01-01';

-- Update with calculations
UPDATE products SET price = price * 1.1 WHERE category = 'electronics';
```

**Real-World Example:**
Like editing a contact in your phone - you change the information but keep the same contact entry.

### Safe UPDATE Practices

**Always Use WHERE Clause:**
```sql
-- DANGEROUS: Updates ALL records
UPDATE users SET status = 'inactive';

-- SAFE: Updates only specific records
UPDATE users SET status = 'inactive' WHERE id = 5;
```

**Using LIMIT for Safety:**
```sql
-- Limit the number of records updated
UPDATE users SET status = 'active' WHERE status = 'pending' LIMIT 10;
```

---

## DELETE Statement - Removing Data

**Definition:**
The DELETE statement removes records from a table.

### Basic DELETE Syntax

**Deleting Specific Records:**
```sql
-- Delete user with specific ID
DELETE FROM users WHERE id = 5;

-- Delete users with specific condition
DELETE FROM users WHERE email LIKE '%@olddomain.com';
```

**Real-World Example:**
Like removing a contact from your phone - you select the contact and delete it.

### Safe DELETE Practices

**Always Use WHERE Clause:**
```sql
-- DANGEROUS: Deletes ALL records
DELETE FROM users;

-- SAFE: Deletes only specific records
DELETE FROM users WHERE id = 5;
```

**Using LIMIT for Safety:**
```sql
-- Delete only first 5 matching records
DELETE FROM users WHERE status = 'inactive' LIMIT 5;
```

**Soft Delete Alternative:**
```sql
-- Instead of deleting, mark as deleted
UPDATE users SET deleted_at = NOW() WHERE id = 5;

-- Then filter out deleted records in queries
SELECT * FROM users WHERE deleted_at IS NULL;
```

---

## WHERE Clause - Filtering Data

**Definition:**
The WHERE clause filters records based on specified conditions.

### Basic WHERE Syntax

**Simple Conditions:**
```sql
-- Equal to
SELECT * FROM users WHERE name = 'John Doe';

-- Not equal to
SELECT * FROM users WHERE status != 'inactive';

-- Greater than
SELECT * FROM products WHERE price > 100;

-- Less than or equal to
SELECT * FROM orders WHERE total <= 50.00;
```

**Real-World Example:**
Like using filters in an online store - you select "price under $50" and "electronics category" to see only relevant products.

### Complex WHERE Conditions

**Multiple Conditions with AND/OR:**
```sql
-- AND condition (both must be true)
SELECT * FROM users WHERE age >= 18 AND status = 'active';

-- OR condition (either can be true)
SELECT * FROM products WHERE category = 'electronics' OR price < 100;

-- Combining AND and OR
SELECT * FROM users WHERE (age >= 18 AND status = 'active') OR role = 'admin';
```

**Using IN and NOT IN:**
```sql
-- IN operator (matches any value in list)
SELECT * FROM users WHERE status IN ('active', 'pending');

-- NOT IN operator
SELECT * FROM products WHERE category NOT IN ('electronics', 'clothing');
```

**Pattern Matching with LIKE:**
```sql
-- Starts with
SELECT * FROM users WHERE name LIKE 'John%';

-- Ends with
SELECT * FROM users WHERE email LIKE '%@gmail.com';

-- Contains
SELECT * FROM products WHERE name LIKE '%phone%';

-- Single character wildcard
SELECT * FROM users WHERE name LIKE 'J_n%';
```

---

## ORDER BY - Sorting Results

**Definition:**
The ORDER BY clause sorts the results of a query in ascending or descending order.

### Basic ORDER BY Syntax

**Single Column Sorting:**
```sql
-- Ascending order (default)
SELECT * FROM users ORDER BY name;

-- Descending order
SELECT * FROM users ORDER BY name DESC;

-- Explicit ascending order
SELECT * FROM products ORDER BY price ASC;
```

**Real-World Example:**
Like sorting your music playlist by artist name or song title - you can arrange it alphabetically or reverse alphabetically.

### Multiple Column Sorting

**Sorting by Multiple Columns:**
```sql
-- Sort by category first, then by price
SELECT * FROM products ORDER BY category, price;

-- Different directions for different columns
SELECT * FROM users ORDER BY status ASC, created_at DESC;
```

**Sorting with NULL Values:**
```sql
-- NULL values appear first
SELECT * FROM users ORDER BY last_login ASC;

-- NULL values appear last
SELECT * FROM users ORDER BY last_login DESC;
```

---

## LIMIT and OFFSET - Controlling Results

**Definition:**
LIMIT restricts the number of rows returned, and OFFSET skips a specified number of rows.

### Basic LIMIT Syntax

**Limiting Results:**
```sql
-- Get only first 10 users
SELECT * FROM users LIMIT 10;

-- Get only first 5 products
SELECT * FROM products ORDER BY price LIMIT 5;
```

**Real-World Example:**
Like asking for only the first 10 results from a search engine - you don't want to see all millions of results at once.

### Using OFFSET for Pagination

**Basic Pagination:**
```sql
-- First page (records 1-10)
SELECT * FROM users LIMIT 10 OFFSET 0;

-- Second page (records 11-20)
SELECT * FROM users LIMIT 10 OFFSET 10;

-- Third page (records 21-30)
SELECT * FROM users LIMIT 10 OFFSET 20;
```

**Alternative Syntax:**
```sql
-- Same as LIMIT 10 OFFSET 20
SELECT * FROM users LIMIT 20, 10;
```

**Practical Pagination Example:**
```sql
-- Page 1: Most recent users
SELECT * FROM users ORDER BY created_at DESC LIMIT 10 OFFSET 0;

-- Page 2: Next 10 most recent users
SELECT * FROM users ORDER BY created_at DESC LIMIT 10 OFFSET 10;
```

---

## Working with NULL Values

**Definition:**
NULL represents missing or unknown data in MySQL. It's different from empty strings or zero values.

### Understanding NULL

**NULL vs Empty String:**
```sql
-- NULL means "no value"
-- Empty string means "empty but exists"

-- Check for NULL
SELECT * FROM users WHERE phone IS NULL;

-- Check for NOT NULL
SELECT * FROM users WHERE phone IS NOT NULL;

-- Check for empty string
SELECT * FROM users WHERE phone = '';
```

**Real-World Example:**
Like a form where some fields are optional - if someone doesn't fill in their phone number, it's NULL, not an empty string.

### Functions for NULL Handling

**COALESCE Function:**
```sql
-- Returns first non-NULL value
SELECT name, COALESCE(phone, 'No phone') AS phone FROM users;

-- Use default value if NULL
SELECT name, COALESCE(last_login, 'Never logged in') AS last_login FROM users;
```

**IFNULL Function:**
```sql
-- MySQL-specific function (same as COALESCE with 2 arguments)
SELECT name, IFNULL(phone, 'No phone') AS phone FROM users;
```

---

## Data Types in MySQL

**Definition:**
MySQL supports various data types for storing different kinds of information efficiently.

### Numeric Data Types

**Integer Types:**
```sql
-- TINYINT: -128 to 127 (or 0 to 255 unsigned)
-- SMALLINT: -32,768 to 32,767
-- INT: -2,147,483,648 to 2,147,483,647
-- BIGINT: Very large numbers

CREATE TABLE examples (
    id INT AUTO_INCREMENT PRIMARY KEY,
    age TINYINT UNSIGNED,
    score INT
);
```

**Decimal Types:**
```sql
-- DECIMAL: Exact decimal numbers
-- FLOAT: Approximate floating-point
-- DOUBLE: Double-precision floating-point

CREATE TABLE products (
    id INT PRIMARY KEY,
    price DECIMAL(10,2),  -- 10 digits total, 2 after decimal
    rating FLOAT
);
```

### String Data Types

**Character Types:**
```sql
-- CHAR: Fixed-length strings
-- VARCHAR: Variable-length strings
-- TEXT: Large text data

CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(50),
    bio TEXT,
    country_code CHAR(2)
);
```

**Real-World Example:**
- **CHAR(2):** Country codes like 'US', 'UK'
- **VARCHAR(100):** Names, emails
- **TEXT:** Long descriptions, comments

### Date and Time Types

**Date/Time Types:**
```sql
-- DATE: YYYY-MM-DD
-- TIME: HH:MM:SS
-- DATETIME: YYYY-MM-DD HH:MM:SS
-- TIMESTAMP: Unix timestamp

CREATE TABLE events (
    id INT PRIMARY KEY,
    event_date DATE,
    start_time TIME,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## Summary

### What We Learned:
- **SQL syntax** follows specific rules and conventions
- **SELECT** retrieves data from tables
- **INSERT** adds new records to tables
- **UPDATE** modifies existing records
- **DELETE** removes records from tables
- **WHERE** filters data based on conditions
- **ORDER BY** sorts query results
- **LIMIT/OFFSET** controls result size and pagination
- **NULL values** represent missing data
- **Data types** determine how information is stored

### Key Analogies:
- **SQL Statements** = Instructions to a librarian
- **WHERE Clause** = Filters in an online store
- **ORDER BY** = Sorting a music playlist
- **LIMIT** = Asking for only first 10 search results
- **NULL Values** = Optional fields in a form
- **Data Types** = Different containers for different items

### Next Steps:
In the next chapter, we'll learn about **database design and normalization** to create efficient database structures!

---

## Practice Questions

1. What are the basic syntax rules for SQL statements?
2. How do you select specific columns from a table?
3. What's the difference between INSERT with column names vs without?
4. Why is it important to always use WHERE clause with UPDATE and DELETE?
5. How do you filter records that contain a specific word using LIKE?
6. What's the difference between ORDER BY ASC and ORDER BY DESC?
7. How do you implement pagination using LIMIT and OFFSET?
8. What's the difference between NULL and an empty string?
9. When would you use CHAR vs VARCHAR data types?
10. How do you handle NULL values in queries using COALESCE?

---

**Ready for Chapter 4? Let's learn about database design and normalization!**

# Chapter 4: Database Design and Normalization

## Table of Contents
- [Understanding Database Design](#understanding-database-design)
- [Entity Relationship Diagrams (ERD)](#entity-relationship-diagrams-erd)
- [Database Normalization](#database-normalization)
- [First Normal Form (1NF)](#first-normal-form-1nf)
- [Second Normal Form (2NF)](#second-normal-form-2nf)
- [Third Normal Form (3NF)](#third-normal-form-3nf)
- [Primary Keys and Foreign Keys](#primary-keys-and-foreign-keys)
- [Indexes and Performance](#indexes-and-performance)
- [Designing for Scalability](#designing-for-scalability)

---

## Understanding Database Design

**Definition:**
Database design is the process of creating a logical and physical structure for storing and organizing data efficiently.

### Why Good Design Matters

**Benefits of Good Design:**
- **Data Integrity:** Ensures data accuracy and consistency
- **Performance:** Faster queries and better efficiency
- **Maintainability:** Easier to modify and extend
- **Scalability:** Can handle growth without major changes

**Real-World Example:**
Like designing a house - you need a solid foundation, proper room layout, and good plumbing to avoid problems later.

### Design Principles

**Key Principles:**
1. **Eliminate Redundancy:** Don't store the same data multiple times
2. **Ensure Data Integrity:** Maintain accuracy and consistency
3. **Optimize for Performance:** Design for efficient queries
4. **Plan for Growth:** Consider future needs

**Analogy:**
Think of database design like organizing a library - you need to decide how to categorize books, where to place them, and how to find them quickly.

---

## Entity Relationship Diagrams (ERD)

**Definition:**
An Entity Relationship Diagram is a visual representation of the database structure showing entities (tables), their attributes (columns), and relationships between them.

### Basic ERD Components

**Entities (Tables):**
- Represent real-world objects (users, products, orders)
- Shown as rectangles in ERD

**Attributes (Columns):**
- Properties of entities (name, email, price)
- Listed inside the entity rectangle

**Relationships:**
- Connections between entities
- Shown as lines with symbols

**Real-World Example:**
Like a blueprint for a building - it shows all the rooms (entities), their features (attributes), and how they connect (relationships).

### ERD Example: E-commerce System

```
┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│   Users     │         │   Orders    │         │  Products   │
├─────────────┤         ├─────────────┤         ├─────────────┤
│ id (PK)     │         │ id (PK)     │         │ id (PK)     │
│ name        │         │ user_id (FK)│         │ name        │
│ email       │         │ total       │         │ price       │
│ created_at  │         │ status      │         │ category    │
└─────────────┘         └─────────────┘         └─────────────┘
        │                       │                       │
        │                       │                       │
        └─────────── 1:N ───────┘                       │
                                    ┌─────────────┐     │
                                    │Order_Items  │     │
                                    ├─────────────┤     │
                                    │order_id (FK)│─────┘
                                    │product_id(FK)│
                                    │quantity     │
                                    │price        │
                                    └─────────────┘
```

**Relationship Types:**
- **1:1 (One-to-One):** One user has one profile
- **1:N (One-to-Many):** One user has many orders
- **M:N (Many-to-Many):** Many users can buy many products

---

## Database Normalization

**Definition:**
Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity.

### Why Normalize?

**Problems with Poor Design:**
- **Data Redundancy:** Same information stored multiple times
- **Update Anomalies:** Changes in one place don't update everywhere
- **Insert Anomalies:** Can't add data without other data
- **Delete Anomalies:** Deleting one record removes needed data

**Real-World Example:**
Like having multiple copies of the same document - when you update one, the others become outdated.

### Normalization Levels

**Normal Forms:**
1. **First Normal Form (1NF):** Eliminate repeating groups
2. **Second Normal Form (2NF):** Remove partial dependencies
3. **Third Normal Form (3NF):** Remove transitive dependencies

**Analogy:**
Like organizing a filing cabinet - first you separate different types of documents (1NF), then organize them by category (2NF), then remove any cross-references (3NF).

---

## First Normal Form (1NF)

**Definition:**
A table is in 1NF if it contains only atomic (indivisible) values and no repeating groups.

### Requirements for 1NF

**Rules:**
1. **Atomic Values:** Each cell contains only one value
2. **No Repeating Groups:** No arrays or lists in single cells
3. **Unique Column Names:** Each column has a unique name
4. **No Duplicate Rows:** Each row is unique

### Example: Violating 1NF

**Bad Design (Not 1NF):**
```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    phones VARCHAR(200)  -- Multiple phone numbers in one field
);

-- Data like: "555-1234, 555-5678, 555-9012"
```

**Good Design (1NF):**
```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE user_phones (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    phone VARCHAR(20),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

**Real-World Example:**
Like separating a list of ingredients into individual items instead of having "flour, sugar, eggs" all in one field.

---

## Second Normal Form (2NF)

**Definition:**
A table is in 2NF if it's in 1NF and all non-key attributes depend on the entire primary key.

### Understanding Partial Dependencies

**Problem:**
When a non-key attribute depends on only part of a composite primary key.

**Example:**
```sql
-- Bad Design (Not 2NF)
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    product_name VARCHAR(100),  -- Depends only on product_id
    product_price DECIMAL(10,2), -- Depends only on product_id
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);
```

**Solution (2NF):**
```sql
-- Separate into two tables
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    product_price DECIMAL(10,2)
);

CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

**Real-World Example:**
Like separating a restaurant menu into dishes (products) and orders (order_items) instead of repeating dish information in every order.

---

## Third Normal Form (3NF)

**Definition:**
A table is in 3NF if it's in 2NF and no non-key attribute depends on another non-key attribute.

### Understanding Transitive Dependencies

**Problem:**
When a non-key attribute depends on another non-key attribute.

**Example:**
```sql
-- Bad Design (Not 3NF)
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    department_name VARCHAR(100),  -- Depends on department_id
    department_location VARCHAR(100) -- Depends on department_id
);
```

**Solution (3NF):**
```sql
-- Separate into two tables
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100),
    department_location VARCHAR(100)
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);
```

**Real-World Example:**
Like separating employee information from department information instead of repeating department details for every employee.

---

## Primary Keys and Foreign Keys

**Definition:**
Primary keys uniquely identify records, while foreign keys create relationships between tables.

### Primary Keys

**Characteristics:**
- **Unique:** No two records can have the same primary key
- **Not NULL:** Must have a value
- **Stable:** Shouldn't change frequently

**Types of Primary Keys:**
```sql
-- Natural Key (business meaning)
CREATE TABLE countries (
    country_code CHAR(2) PRIMARY KEY,  -- 'US', 'UK', etc.
    country_name VARCHAR(100)
);

-- Surrogate Key (auto-generated)
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,  -- 1, 2, 3, etc.
    email VARCHAR(100) UNIQUE
);
```

**Real-World Example:**
Like a social security number (natural key) vs a library card number (surrogate key).

### Foreign Keys

**Purpose:**
- **Referential Integrity:** Ensures data consistency
- **Relationships:** Links tables together
- **Constraints:** Prevents invalid references

**Example:**
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    total DECIMAL(10,2),
    FOREIGN KEY (user_id) REFERENCES users(id)
        ON DELETE CASCADE  -- Delete orders when user is deleted
        ON UPDATE CASCADE  -- Update orders when user ID changes
);
```

**Foreign Key Actions:**
- **CASCADE:** Automatically update/delete related records
- **SET NULL:** Set foreign key to NULL
- **RESTRICT:** Prevent the action if related records exist

---

## Indexes and Performance

**Definition:**
Indexes are data structures that improve the speed of data retrieval operations.

### How Indexes Work

**Analogy:**
Like the index in a book - instead of reading every page to find a topic, you look it up in the index and go directly to the right page.

**Types of Indexes:**
```sql
-- Single-column index
CREATE INDEX idx_user_email ON users(email);

-- Composite index (multiple columns)
CREATE INDEX idx_user_name_email ON users(name, email);

-- Unique index
CREATE UNIQUE INDEX idx_user_email_unique ON users(email);
```

### When to Use Indexes

**Good Candidates for Indexing:**
- **Primary Keys:** Automatically indexed
- **Foreign Keys:** Often need indexes for joins
- **Frequently Searched Columns:** WHERE clause columns
- **Sorting Columns:** ORDER BY columns

**Example:**
```sql
-- Without index (slow)
SELECT * FROM users WHERE email = 'john@example.com';

-- With index (fast)
CREATE INDEX idx_email ON users(email);
SELECT * FROM users WHERE email = 'john@example.com';
```

### Index Considerations

**Trade-offs:**
- **Pros:** Faster queries, better performance
- **Cons:** Slower INSERT/UPDATE/DELETE, more storage space

**Best Practices:**
- Index columns used in WHERE, JOIN, ORDER BY
- Don't over-index (too many indexes slow down writes)
- Monitor index usage and remove unused indexes

---

## Designing for Scalability

**Definition:**
Scalable design allows the database to handle growth in data volume and user load.

### Horizontal vs Vertical Scaling

**Vertical Scaling:**
- **Definition:** Adding more resources to the same server
- **Example:** More RAM, faster CPU, larger storage
- **Limitations:** Hardware limits, single point of failure

**Horizontal Scaling:**
- **Definition:** Adding more servers to distribute load
- **Example:** Database sharding, read replicas
- **Benefits:** Better performance, high availability

### Design Patterns for Scalability

**1. Partitioning:**
```sql
-- Partition tables by date
CREATE TABLE orders_2023 (
    -- same structure as orders
) PARTITION BY RANGE (YEAR(order_date)) (
    PARTITION p2023 VALUES LESS THAN (2024),
    PARTITION p2024 VALUES LESS THAN (2025)
);
```

**2. Read Replicas:**
- **Primary:** Handles writes
- **Replicas:** Handle reads
- **Benefits:** Distribute read load

**3. Caching:**
- **Application Cache:** Store frequently accessed data
- **Query Cache:** Cache query results
- **Benefits:** Reduce database load

### Performance Optimization

**Query Optimization:**
```sql
-- Use EXPLAIN to analyze queries
EXPLAIN SELECT * FROM users WHERE email = 'john@example.com';

-- Optimize slow queries
-- Add indexes, rewrite queries, use appropriate data types
```

**Monitoring:**
- **Slow Query Log:** Identify problematic queries
- **Performance Schema:** Monitor database performance
- **Regular Maintenance:** Analyze and optimize tables

---

## Summary

### What We Learned:
- **Database design** is crucial for performance and maintainability
- **ERDs** provide visual representation of database structure
- **Normalization** reduces redundancy and improves data integrity
- **Primary and foreign keys** ensure data relationships
- **Indexes** improve query performance
- **Scalable design** prepares for future growth

### Key Analogies:
- **Database Design** = Building a house with proper foundation
- **ERDs** = Blueprint showing room layout and connections
- **Normalization** = Organizing a filing cabinet properly
- **Primary Keys** = Social security numbers for records
- **Foreign Keys** = References between related documents
- **Indexes** = Book index for quick lookups
- **Scaling** = Adding more lanes to a highway

### Next Steps:
In the next chapter, we'll learn about **advanced SQL queries and joins** to work with multiple tables!

---

## Practice Questions

1. What are the benefits of good database design?
2. Explain the three types of relationships in ERDs with examples.
3. What problems does normalization solve?
4. How do you identify if a table violates 1NF?
5. What is a partial dependency and how does 2NF fix it?
6. Explain transitive dependencies and how 3NF addresses them.
7. What's the difference between natural and surrogate primary keys?
8. When should you create indexes on database columns?
9. What are the trade-offs of using indexes?
10. How does horizontal scaling differ from vertical scaling?

---

**Ready for Chapter 5? Let's learn advanced SQL queries and joins!**

# Chapter 5: Advanced SQL Queries and Joins

## Table of Contents
- [Understanding SQL Joins](#understanding-sql-joins)
- [INNER JOIN](#inner-join)
- [LEFT JOIN and RIGHT JOIN](#left-join-and-right-join)
- [FULL OUTER JOIN](#full-outer-join)
- [CROSS JOIN](#cross-join)
- [Self Joins](#self-joins)
- [Aggregate Functions](#aggregate-functions)
- [GROUP BY and HAVING](#group-by-and-having)
- [Subqueries](#subqueries)
- [Common Table Expressions (CTEs)](#common-table-expressions-ctes)
- [Window Functions](#window-functions)

---

## Understanding SQL Joins

**Definition:**
SQL joins combine data from multiple tables based on related columns, allowing you to retrieve data that spans across different tables.

### Why Use Joins?

**Purpose:**
- **Combine Related Data:** Get information from multiple tables in one query
- **Maintain Data Integrity:** Keep data normalized while still accessing related information
- **Efficient Queries:** Retrieve complex data relationships efficiently

**Real-World Example:**
Like looking up a customer's order history - you need to connect customer information with their orders to see what they've purchased.

### Join Types Overview

**Main Join Types:**
1. **INNER JOIN:** Only matching records from both tables
2. **LEFT JOIN:** All records from left table + matching from right
3. **RIGHT JOIN:** All records from right table + matching from left
4. **FULL OUTER JOIN:** All records from both tables
5. **CROSS JOIN:** Every record from first table with every record from second

**Analogy:**
Think of joins like connecting puzzle pieces - different join types determine which pieces you include in the final picture.

---

## INNER JOIN

**Definition:**
INNER JOIN returns only the records that have matching values in both tables.

### Basic INNER JOIN Syntax

**Simple Join:**
```sql
-- Join users with their orders
SELECT users.name, orders.order_date, orders.total
FROM users
INNER JOIN orders ON users.id = orders.user_id;
```

**Real-World Example:**
Like finding all customers who have placed orders - you only want customers who actually have order history.

### Multiple Table Joins

**Joining Three Tables:**
```sql
-- Get user name, product name, and order details
SELECT 
    users.name AS customer_name,
    products.name AS product_name,
    order_items.quantity,
    order_items.price
FROM users
INNER JOIN orders ON users.id = orders.user_id
INNER JOIN order_items ON orders.id = order_items.order_id
INNER JOIN products ON order_items.product_id = products.id;
```

**Join Order Matters:**
```sql
-- These produce the same result
SELECT * FROM table1 
INNER JOIN table2 ON table1.id = table2.id
INNER JOIN table3 ON table2.id = table3.id;

SELECT * FROM table1 
INNER JOIN table3 ON table1.id = table3.id
INNER JOIN table2 ON table1.id = table2.id;
```

### INNER JOIN with WHERE Clause

**Filtering Joined Results:**
```sql
-- Get orders for specific user
SELECT orders.*, users.name
FROM orders
INNER JOIN users ON orders.user_id = users.id
WHERE users.email = 'john@example.com';

-- Get recent orders with user info
SELECT orders.*, users.name
FROM orders
INNER JOIN users ON orders.user_id = users.id
WHERE orders.order_date >= '2023-01-01'
ORDER BY orders.order_date DESC;
```

---

## LEFT JOIN and RIGHT JOIN

**Definition:**
LEFT JOIN returns all records from the left table and matching records from the right table. RIGHT JOIN does the opposite.

### LEFT JOIN

**Basic LEFT JOIN:**
```sql
-- Get all users and their orders (if any)
SELECT users.name, orders.order_date, orders.total
FROM users
LEFT JOIN orders ON users.id = orders.user_id;
```

**Real-World Example:**
Like getting a list of all customers, including those who haven't placed any orders yet.

### Finding Records Without Matches

**Using LEFT JOIN to Find Missing Data:**
```sql
-- Find users who haven't placed any orders
SELECT users.name, users.email
FROM users
LEFT JOIN orders ON users.id = orders.user_id
WHERE orders.id IS NULL;
```

**Finding Orphaned Records:**
```sql
-- Find orders without valid users
SELECT orders.*
FROM orders
LEFT JOIN users ON orders.user_id = users.id
WHERE users.id IS NULL;
```

### RIGHT JOIN

**Basic RIGHT JOIN:**
```sql
-- Get all orders and user info (if user exists)
SELECT orders.*, users.name
FROM users
RIGHT JOIN orders ON users.id = orders.user_id;
```

**When to Use RIGHT JOIN:**
```sql
-- Same as LEFT JOIN with tables swapped
SELECT orders.*, users.name
FROM orders
LEFT JOIN users ON orders.user_id = users.id;
```

**Real-World Example:**
RIGHT JOIN is less commonly used because you can usually achieve the same result by swapping table order in LEFT JOIN.

---

## FULL OUTER JOIN

**Definition:**
FULL OUTER JOIN returns all records from both tables, including unmatched records from either table.

### Basic FULL OUTER JOIN

**Syntax:**
```sql
-- Get all users and all orders, matched where possible
SELECT users.name, orders.order_date
FROM users
FULL OUTER JOIN orders ON users.id = orders.user_id;
```

**Note:** MySQL doesn't support FULL OUTER JOIN directly, but you can simulate it:

**Simulating FULL OUTER JOIN in MySQL:**
```sql
-- Using UNION to simulate FULL OUTER JOIN
SELECT users.name, orders.order_date
FROM users
LEFT JOIN orders ON users.id = orders.user_id

UNION

SELECT users.name, orders.order_date
FROM users
RIGHT JOIN orders ON users.id = orders.user_id
WHERE users.id IS NULL;
```

**Real-World Example:**
Like getting a complete picture of all customers and all orders, even if some customers have no orders and some orders have no customers.

---

## CROSS JOIN

**Definition:**
CROSS JOIN returns the Cartesian product of two tables - every row from the first table paired with every row from the second table.

### Basic CROSS JOIN

**Simple CROSS JOIN:**
```sql
-- Get all combinations of users and products
SELECT users.name, products.name
FROM users
CROSS JOIN products;
```

**Real-World Example:**
Like creating a matrix of all possible combinations - useful for generating test data or finding all possible pairings.

### When to Use CROSS JOIN

**Use Cases:**
```sql
-- Generate date ranges
SELECT 
    start_date.date AS start_date,
    end_date.date AS end_date
FROM (
    SELECT '2023-01-01' AS date UNION ALL
    SELECT '2023-01-02' UNION ALL
    SELECT '2023-01-03'
) AS start_date
CROSS JOIN (
    SELECT '2023-01-01' AS date UNION ALL
    SELECT '2023-01-02' UNION ALL
    SELECT '2023-01-03'
) AS end_date
WHERE start_date.date <= end_date.date;
```

**Warning:**
CROSS JOIN can produce very large result sets - use with caution on large tables.

---

## Self Joins

**Definition:**
A self join is when a table is joined with itself, typically to compare rows within the same table.

### Basic Self Join

**Employee Hierarchy Example:**
```sql
-- Find employees and their managers
SELECT 
    e1.name AS employee_name,
    e2.name AS manager_name
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.id;
```

**Real-World Example:**
Like finding who reports to whom in an organization chart.

### Self Join for Comparisons

**Finding Similar Records:**
```sql
-- Find products with similar prices
SELECT 
    p1.name AS product1,
    p2.name AS product2,
    p1.price
FROM products p1
INNER JOIN products p2 ON p1.price = p2.price
WHERE p1.id < p2.id;  -- Avoid duplicate pairs
```

**Finding Records Within Range:**
```sql
-- Find users who registered within 30 days of each other
SELECT 
    u1.name AS user1,
    u2.name AS user2,
    DATEDIFF(u1.created_at, u2.created_at) AS days_difference
FROM users u1
INNER JOIN users u2 ON 
    ABS(DATEDIFF(u1.created_at, u2.created_at)) <= 30
WHERE u1.id < u2.id;
```

---

## Aggregate Functions

**Definition:**
Aggregate functions perform calculations on sets of values and return a single result.

### Common Aggregate Functions

**Basic Aggregates:**
```sql
-- Count records
SELECT COUNT(*) FROM users;

-- Sum values
SELECT SUM(total) FROM orders;

-- Average values
SELECT AVG(price) FROM products;

-- Maximum value
SELECT MAX(price) FROM products;

-- Minimum value
SELECT MIN(price) FROM products;
```

**Real-World Example:**
Like calculating statistics - total sales, average order value, number of customers.

### Aggregate Functions with Conditions

**Using WHERE with Aggregates:**
```sql
-- Count active users
SELECT COUNT(*) FROM users WHERE status = 'active';

-- Average order value for specific user
SELECT AVG(total) FROM orders WHERE user_id = 5;

-- Total sales in specific period
SELECT SUM(total) FROM orders 
WHERE order_date BETWEEN '2023-01-01' AND '2023-12-31';
```

### Multiple Aggregates

**Combining Functions:**
```sql
-- Get comprehensive order statistics
SELECT 
    COUNT(*) AS total_orders,
    SUM(total) AS total_revenue,
    AVG(total) AS average_order_value,
    MIN(total) AS smallest_order,
    MAX(total) AS largest_order
FROM orders;
```

---

## GROUP BY and HAVING

**Definition:**
GROUP BY groups rows by specified columns, and HAVING filters groups based on aggregate conditions.

### Basic GROUP BY

**Grouping by Single Column:**
```sql
-- Count orders per user
SELECT user_id, COUNT(*) AS order_count
FROM orders
GROUP BY user_id;
```

**Grouping by Multiple Columns:**
```sql
-- Count orders per user per month
SELECT 
    user_id,
    YEAR(order_date) AS year,
    MONTH(order_date) AS month,
    COUNT(*) AS order_count
FROM orders
GROUP BY user_id, YEAR(order_date), MONTH(order_date);
```

**Real-World Example:**
Like creating a summary report - instead of seeing individual orders, you see totals by category.

### Using HAVING

**Filtering Groups:**
```sql
-- Find users with more than 5 orders
SELECT user_id, COUNT(*) AS order_count
FROM orders
GROUP BY user_id
HAVING COUNT(*) > 5;
```

**HAVING vs WHERE:**
```sql
-- WHERE filters individual rows
SELECT user_id, COUNT(*) AS order_count
FROM orders
WHERE total > 100  -- Only orders over $100
GROUP BY user_id;

-- HAVING filters groups
SELECT user_id, COUNT(*) AS order_count
FROM orders
GROUP BY user_id
HAVING COUNT(*) > 5;  -- Only users with more than 5 orders
```

### Complex GROUP BY Examples

**Sales Analysis:**
```sql
-- Monthly sales by product category
SELECT 
    p.category,
    YEAR(o.order_date) AS year,
    MONTH(o.order_date) AS month,
    COUNT(*) AS orders,
    SUM(oi.quantity) AS units_sold,
    SUM(oi.quantity * oi.price) AS revenue
FROM orders o
INNER JOIN order_items oi ON o.id = oi.order_id
INNER JOIN products p ON oi.product_id = p.id
GROUP BY p.category, YEAR(o.order_date), MONTH(o.order_date)
ORDER BY year, month, revenue DESC;
```

---

## Subqueries

**Definition:**
Subqueries are queries nested inside other queries, allowing you to use the result of one query in another.

### Types of Subqueries

**Scalar Subqueries (Single Value):**
```sql
-- Find products more expensive than average
SELECT name, price
FROM products
WHERE price > (SELECT AVG(price) FROM products);
```

**Column Subqueries (Multiple Values):**
```sql
-- Find users who placed orders
SELECT name, email
FROM users
WHERE id IN (SELECT DISTINCT user_id FROM orders);
```

**Table Subqueries (Multiple Columns):**
```sql
-- Find top customers
SELECT u.name, u.email, total_orders
FROM users u
INNER JOIN (
    SELECT user_id, COUNT(*) AS total_orders
    FROM orders
    GROUP BY user_id
    ORDER BY COUNT(*) DESC
    LIMIT 10
) AS top_customers ON u.id = top_customers.user_id;
```

### Subqueries in Different Clauses

**In SELECT Clause:**
```sql
-- Add average price to each product
SELECT 
    name,
    price,
    (SELECT AVG(price) FROM products) AS avg_price,
    price - (SELECT AVG(price) FROM products) AS price_diff
FROM products;
```

**In FROM Clause:**
```sql
-- Use subquery as a table
SELECT category, COUNT(*) AS product_count
FROM (
    SELECT 
        CASE 
            WHEN price < 50 THEN 'Budget'
            WHEN price < 200 THEN 'Mid-range'
            ELSE 'Premium'
        END AS category
    FROM products
) AS categorized_products
GROUP BY category;
```

**In WHERE Clause:**
```sql
-- Find products with no orders
SELECT name
FROM products
WHERE id NOT IN (SELECT DISTINCT product_id FROM order_items);
```

---

## Common Table Expressions (CTEs)

**Definition:**
CTEs are temporary named result sets that exist only within the scope of a single SQL statement.

### Basic CTE Syntax

**Simple CTE:**
```sql
WITH user_orders AS (
    SELECT user_id, COUNT(*) AS order_count
    FROM orders
    GROUP BY user_id
)
SELECT u.name, uo.order_count
FROM users u
INNER JOIN user_orders uo ON u.id = uo.user_id;
```

**Real-World Example:**
Like creating a temporary worksheet that you use for calculations, then discard.

### Multiple CTEs

**Chaining CTEs:**
```sql
WITH 
    user_totals AS (
        SELECT user_id, SUM(total) AS total_spent
        FROM orders
        GROUP BY user_id
    ),
    top_spenders AS (
        SELECT user_id, total_spent
        FROM user_totals
        WHERE total_spent > 1000
    )
SELECT u.name, ts.total_spent
FROM users u
INNER JOIN top_spenders ts ON u.id = ts.user_id
ORDER BY ts.total_spent DESC;
```

### Recursive CTEs

**Hierarchical Data:**
```sql
WITH RECURSIVE employee_hierarchy AS (
    -- Base case: top-level employees (no manager)
    SELECT id, name, manager_id, 1 AS level
    FROM employees
    WHERE manager_id IS NULL
    
    UNION ALL
    
    -- Recursive case: employees with managers
    SELECT e.id, e.name, e.manager_id, eh.level + 1
    FROM employees e
    INNER JOIN employee_hierarchy eh ON e.manager_id = eh.id
)
SELECT * FROM employee_hierarchy;
```

---

## Window Functions

**Definition:**
Window functions perform calculations across a set of table rows related to the current row.

### Basic Window Functions

**ROW_NUMBER():**
```sql
-- Rank products by price
SELECT 
    name,
    price,
    ROW_NUMBER() OVER (ORDER BY price DESC) AS price_rank
FROM products;
```

**RANK() and DENSE_RANK():**
```sql
-- Rank users by total spending
SELECT 
    u.name,
    SUM(o.total) AS total_spent,
    RANK() OVER (ORDER BY SUM(o.total) DESC) AS rank,
    DENSE_RANK() OVER (ORDER BY SUM(o.total) DESC) AS dense_rank
FROM users u
INNER JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.name;
```

### Partitioning with Window Functions

**Partitioned Rankings:**
```sql
-- Rank products within each category
SELECT 
    name,
    category,
    price,
    ROW_NUMBER() OVER (PARTITION BY category ORDER BY price DESC) AS category_rank
FROM products;
```

**Running Totals:**
```sql
-- Calculate running total of orders
SELECT 
    order_date,
    total,
    SUM(total) OVER (ORDER BY order_date) AS running_total
FROM orders
ORDER BY order_date;
```

### Advanced Window Functions

**Moving Averages:**
```sql
-- 7-day moving average of daily sales
SELECT 
    order_date,
    daily_sales,
    AVG(daily_sales) OVER (
        ORDER BY order_date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS moving_avg_7d
FROM (
    SELECT 
        DATE(order_date) AS order_date,
        SUM(total) AS daily_sales
    FROM orders
    GROUP BY DATE(order_date)
) AS daily_totals;
```

---

## Summary

### What We Learned:
- **SQL joins** combine data from multiple tables
- **INNER JOIN** returns only matching records
- **LEFT/RIGHT JOIN** includes all records from one table
- **Aggregate functions** perform calculations on data sets
- **GROUP BY** groups data for analysis
- **Subqueries** nest queries within queries
- **CTEs** create temporary result sets
- **Window functions** perform calculations across rows

### Key Analogies:
- **Joins** = Connecting puzzle pieces
- **INNER JOIN** = Only matching pieces
- **LEFT JOIN** = All left pieces + matching right pieces
- **Aggregates** = Calculating statistics
- **GROUP BY** = Creating summary reports
- **Subqueries** = Nested questions
- **CTEs** = Temporary worksheets
- **Window Functions** = Calculations across related rows

### Next Steps:
In the next chapter, we'll learn how to **integrate MySQL with Node.js and Express**!

---

## Practice Questions

1. What's the difference between INNER JOIN and LEFT JOIN?
2. When would you use a self join? Give an example.
3. How do you simulate FULL OUTER JOIN in MySQL?
4. What's the difference between WHERE and HAVING clauses?
5. How do you find records that don't have matches using LEFT JOIN?
6. What are the main aggregate functions in SQL?
7. How do you use subqueries in the WHERE clause?
8. What's the difference between RANK() and DENSE_RANK()?
9. When would you use a CTE instead of a subquery?
10. How do you calculate a running total using window functions?

---

**Ready for Chapter 6? Let's learn how to integrate MySQL with Node.js and Express!**

# Chapter 6: MySQL with Node.js and Express

## Table of Contents
- [Setting Up MySQL with Node.js](#setting-up-mysql-with-nodejs)
- [Using mysql2 Package](#using-mysql2-package)
- [Connection Pooling](#connection-pooling)
- [Basic CRUD Operations](#basic-crud-operations)
- [Error Handling and Security](#error-handling-and-security)
- [Prepared Statements](#prepared-statements)
- [Transactions](#transactions)
- [Building REST APIs with MySQL](#building-rest-apis-with-mysql)
- [Best Practices](#best-practices)

---

## Setting Up MySQL with Node.js

**Definition:**
Integrating MySQL with Node.js allows you to build web applications that can store and retrieve data from a MySQL database.

### Required Packages

**Installation:**
```bash
# Create a new Node.js project
npm init -y

# Install required packages
npm install express mysql2 dotenv
```

**Package Purposes:**
- **express:** Web framework for building APIs
- **mysql2:** MySQL driver for Node.js
- **dotenv:** Load environment variables

**Real-World Example:**
Like connecting your web application to a database - it's like plugging your website into a data storage system.

### Project Structure

**Basic Structure:**
```
my-mysql-app/
├── config/
│   └── database.js
├── routes/
│   └── users.js
├── controllers/
│   └── userController.js
├── .env
├── app.js
└── package.json
```

---

## Using mysql2 Package

**Definition:**
mysql2 is a modern MySQL driver for Node.js that provides better performance and features than the older mysql package.

### Basic Connection Setup

**Database Configuration:**
```javascript
// config/database.js
const mysql = require('mysql2/promise');
require('dotenv').config();

const dbConfig = {
    host: process.env.DB_HOST || 'localhost',
    user: process.env.DB_USER || 'root',
    password: process.env.DB_PASSWORD,
    database: process.env.DB_NAME || 'myapp',
    port: process.env.DB_PORT || 3306
};

// Create connection pool
const pool = mysql.createPool(dbConfig);

module.exports = pool;
```

**Environment Variables (.env):**
```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=myapp
DB_PORT=3306
```

### Testing the Connection

**Connection Test:**
```javascript
// test-connection.js
const pool = require('./config/database');

async function testConnection() {
    try {
        const connection = await pool.getConnection();
        console.log('✅ Database connected successfully!');
        
        // Test a simple query
        const [rows] = await connection.execute('SELECT 1 as test');
        console.log('✅ Query test successful:', rows);
        
        connection.release();
    } catch (error) {
        console.error('❌ Database connection failed:', error.message);
    }
}

testConnection();
```

---

## Connection Pooling

**Definition:**
Connection pooling manages a pool of database connections, reusing them instead of creating new connections for each query.

### Why Use Connection Pooling?

**Benefits:**
- **Performance:** Faster than creating new connections
- **Resource Management:** Limits concurrent connections
- **Reliability:** Handles connection failures gracefully

**Real-World Example:**
Like having a team of workers ready to handle tasks instead of hiring and firing workers for each job.

### Pool Configuration

**Advanced Pool Setup:**
```javascript
// config/database.js
const mysql = require('mysql2/promise');
require('dotenv').config();

const pool = mysql.createPool({
    host: process.env.DB_HOST,
    user: process.env.DB_USER,
    password: process.env.DB_PASSWORD,
    database: process.env.DB_NAME,
    port: process.env.DB_PORT,
    
    // Pool configuration
    connectionLimit: 10,        // Maximum connections
    acquireTimeout: 60000,      // Connection timeout (ms)
    timeout: 60000,            // Query timeout (ms)
    reconnect: true,           // Auto-reconnect
    waitForConnections: true,  // Wait for available connection
    
    // Queue configuration
    queueLimit: 0,             // No limit on queued requests
});

module.exports = pool;
```

### Using the Pool

**Basic Usage:**
```javascript
const pool = require('./config/database');

async function getUsers() {
    try {
        const [rows] = await pool.execute('SELECT * FROM users');
        return rows;
    } catch (error) {
        console.error('Error fetching users:', error);
        throw error;
    }
}
```

---

## Basic CRUD Operations

**Definition:**
CRUD operations (Create, Read, Update, Delete) are the fundamental database operations for managing data.

### Create (INSERT)

**Adding New Records:**
```javascript
// controllers/userController.js
const pool = require('../config/database');

async function createUser(userData) {
    try {
        const { name, email, password } = userData;
        
        const [result] = await pool.execute(
            'INSERT INTO users (name, email, password) VALUES (?, ?, ?)',
            [name, email, password]
        );
        
        return {
            id: result.insertId,
            name,
            email,
            message: 'User created successfully'
        };
    } catch (error) {
        console.error('Error creating user:', error);
        throw error;
    }
}
```

### Read (SELECT)

**Fetching Data:**
```javascript
// Get all users
async function getAllUsers() {
    try {
        const [rows] = await pool.execute('SELECT id, name, email FROM users');
        return rows;
    } catch (error) {
        console.error('Error fetching users:', error);
        throw error;
    }
}

// Get user by ID
async function getUserById(id) {
    try {
        const [rows] = await pool.execute(
            'SELECT id, name, email FROM users WHERE id = ?',
            [id]
        );
        
        return rows.length > 0 ? rows[0] : null;
    } catch (error) {
        console.error('Error fetching user:', error);
        throw error;
    }
}
```

### Update (UPDATE)

**Modifying Records:**
```javascript
async function updateUser(id, userData) {
    try {
        const { name, email } = userData;
        
        const [result] = await pool.execute(
            'UPDATE users SET name = ?, email = ? WHERE id = ?',
            [name, email, id]
        );
        
        if (result.affectedRows === 0) {
            throw new Error('User not found');
        }
        
        return { message: 'User updated successfully' };
    } catch (error) {
        console.error('Error updating user:', error);
        throw error;
    }
}
```

### Delete (DELETE)

**Removing Records:**
```javascript
async function deleteUser(id) {
    try {
        const [result] = await pool.execute(
            'DELETE FROM users WHERE id = ?',
            [id]
        );
        
        if (result.affectedRows === 0) {
            throw new Error('User not found');
        }
        
        return { message: 'User deleted successfully' };
    } catch (error) {
        console.error('Error deleting user:', error);
        throw error;
    }
}
```

---

## Error Handling and Security

**Definition:**
Proper error handling and security measures are crucial for production applications.

### Error Handling

**Comprehensive Error Handling:**
```javascript
// utils/errorHandler.js
class DatabaseError extends Error {
    constructor(message, code) {
        super(message);
        this.name = 'DatabaseError';
        this.code = code;
    }
}

async function handleDatabaseOperation(operation) {
    try {
        return await operation();
    } catch (error) {
        // Handle specific MySQL errors
        switch (error.code) {
            case 'ER_DUP_ENTRY':
                throw new DatabaseError('Duplicate entry found', 'DUPLICATE');
            case 'ER_NO_REFERENCED_ROW_2':
                throw new DatabaseError('Referenced record not found', 'FOREIGN_KEY');
            case 'ER_ROW_IS_REFERENCED_2':
                throw new DatabaseError('Cannot delete referenced record', 'REFERENCED');
            default:
                console.error('Database error:', error);
                throw new DatabaseError('Database operation failed', 'UNKNOWN');
        }
    }
}
```

### Security Best Practices

**Input Validation:**
```javascript
// utils/validation.js
const { body, validationResult } = require('express-validator');

const validateUser = [
    body('name').trim().isLength({ min: 2, max: 100 }).escape(),
    body('email').isEmail().normalizeEmail(),
    body('password').isLength({ min: 6 }),
    
    (req, res, next) => {
        const errors = validationResult(req);
        if (!errors.isEmpty()) {
            return res.status(400).json({ errors: errors.array() });
        }
        next();
    }
];

module.exports = { validateUser };
```

**SQL Injection Prevention:**
```javascript
// ❌ BAD - Vulnerable to SQL injection
const query = `SELECT * FROM users WHERE email = '${email}'`;

// ✅ GOOD - Use prepared statements
const [rows] = await pool.execute(
    'SELECT * FROM users WHERE email = ?',
    [email]
);
```

---

## Prepared Statements

**Definition:**
Prepared statements are pre-compiled SQL statements that can be executed multiple times with different parameters.

### Benefits of Prepared Statements

**Advantages:**
- **Security:** Prevents SQL injection attacks
- **Performance:** Queries are compiled once and reused
- **Reliability:** Reduces parsing errors

**Real-World Example:**
Like having a template for a letter - you fill in the blanks but the structure stays the same.

### Using Prepared Statements

**Basic Prepared Statement:**
```javascript
async function searchUsers(searchTerm) {
    try {
        const [rows] = await pool.execute(
            'SELECT * FROM users WHERE name LIKE ? OR email LIKE ?',
            [`%${searchTerm}%`, `%${searchTerm}%`]
        );
        return rows;
    } catch (error) {
        console.error('Error searching users:', error);
        throw error;
    }
}
```

**Complex Prepared Statement:**
```javascript
async function getUsersWithFilters(filters) {
    try {
        let query = 'SELECT * FROM users WHERE 1=1';
        const params = [];
        
        if (filters.name) {
            query += ' AND name LIKE ?';
            params.push(`%${filters.name}%`);
        }
        
        if (filters.email) {
            query += ' AND email LIKE ?';
            params.push(`%${filters.email}%`);
        }
        
        if (filters.status) {
            query += ' AND status = ?';
            params.push(filters.status);
        }
        
        query += ' ORDER BY created_at DESC LIMIT ? OFFSET ?';
        params.push(filters.limit || 10, filters.offset || 0);
        
        const [rows] = await pool.execute(query, params);
        return rows;
    } catch (error) {
        console.error('Error fetching users with filters:', error);
        throw error;
    }
}
```

---

## Transactions

**Definition:**
Transactions ensure that multiple database operations either all succeed or all fail together, maintaining data consistency.

### Why Use Transactions?

**Benefits:**
- **Data Integrity:** Ensures related operations succeed or fail together
- **Consistency:** Prevents partial updates
- **Isolation:** Operations don't interfere with each other

**Real-World Example:**
Like a bank transfer - both the withdrawal and deposit must succeed, or neither should happen.

### Basic Transaction Example

**Simple Transaction:**
```javascript
async function transferMoney(fromAccountId, toAccountId, amount) {
    const connection = await pool.getConnection();
    
    try {
        await connection.beginTransaction();
        
        // Deduct from source account
        await connection.execute(
            'UPDATE accounts SET balance = balance - ? WHERE id = ? AND balance >= ?',
            [amount, fromAccountId, amount]
        );
        
        // Add to destination account
        await connection.execute(
            'UPDATE accounts SET balance = balance + ? WHERE id = ?',
            [amount, toAccountId]
        );
        
        await connection.commit();
        return { message: 'Transfer completed successfully' };
        
    } catch (error) {
        await connection.rollback();
        console.error('Transfer failed:', error);
        throw error;
    } finally {
        connection.release();
    }
}
```

### Complex Transaction Example

**Order Processing:**
```javascript
async function processOrder(orderData) {
    const connection = await pool.getConnection();
    
    try {
        await connection.beginTransaction();
        
        // Create order
        const [orderResult] = await connection.execute(
            'INSERT INTO orders (user_id, total, status) VALUES (?, ?, ?)',
            [orderData.userId, orderData.total, 'pending']
        );
        
        const orderId = orderResult.insertId;
        
        // Add order items
        for (const item of orderData.items) {
            await connection.execute(
                'INSERT INTO order_items (order_id, product_id, quantity, price) VALUES (?, ?, ?, ?)',
                [orderId, item.productId, item.quantity, item.price]
            );
            
            // Update product stock
            await connection.execute(
                'UPDATE products SET stock = stock - ? WHERE id = ? AND stock >= ?',
                [item.quantity, item.productId, item.quantity]
            );
        }
        
        // Update order status
        await connection.execute(
            'UPDATE orders SET status = ? WHERE id = ?',
            ['completed', orderId]
        );
        
        await connection.commit();
        return { orderId, message: 'Order processed successfully' };
        
    } catch (error) {
        await connection.rollback();
        console.error('Order processing failed:', error);
        throw error;
    } finally {
        connection.release();
    }
}
```

---

## Building REST APIs with MySQL

**Definition:**
REST APIs provide a standardized way to interact with your MySQL database through HTTP requests.

### Express.js Setup

**Basic Express App:**
```javascript
// app.js
const express = require('express');
const userRoutes = require('./routes/users');
require('dotenv').config();

const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Routes
app.use('/api/users', userRoutes);

// Error handling middleware
app.use((error, req, res, next) => {
    console.error('Error:', error);
    res.status(500).json({ 
        error: 'Internal server error',
        message: error.message 
    });
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

### User Routes

**Complete User API:**
```javascript
// routes/users.js
const express = require('express');
const router = express.Router();
const userController = require('../controllers/userController');
const { validateUser } = require('../utils/validation');

// GET all users
router.get('/', async (req, res) => {
    try {
        const users = await userController.getAllUsers();
        res.json(users);
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
});

// GET user by ID
router.get('/:id', async (req, res) => {
    try {
        const user = await userController.getUserById(req.params.id);
        if (!user) {
            return res.status(404).json({ error: 'User not found' });
        }
        res.json(user);
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
});

// POST create user
router.post('/', validateUser, async (req, res) => {
    try {
        const newUser = await userController.createUser(req.body);
        res.status(201).json(newUser);
    } catch (error) {
        res.status(400).json({ error: error.message });
    }
});

// PUT update user
router.put('/:id', validateUser, async (req, res) => {
    try {
        const result = await userController.updateUser(req.params.id, req.body);
        res.json(result);
    } catch (error) {
        res.status(400).json({ error: error.message });
    }
});

// DELETE user
router.delete('/:id', async (req, res) => {
    try {
        const result = await userController.deleteUser(req.params.id);
        res.json(result);
    } catch (error) {
        res.status(400).json({ error: error.message });
    }
});

module.exports = router;
```

### Advanced API Features

**Pagination and Filtering:**
```javascript
// GET users with pagination and filters
router.get('/', async (req, res) => {
    try {
        const { page = 1, limit = 10, search, status } = req.query;
        const offset = (page - 1) * limit;
        
        const filters = {
            search,
            status,
            limit: parseInt(limit),
            offset: parseInt(offset)
        };
        
        const users = await userController.getUsersWithFilters(filters);
        res.json(users);
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
});
```

---

## Best Practices

**Definition:**
Following best practices ensures your MySQL Node.js application is secure, performant, and maintainable.

### Code Organization

**MVC Pattern:**
```javascript
// Model (database operations)
// controllers/userController.js - Contains all database logic

// View (API responses)
// routes/users.js - Handles HTTP requests and responses

// Controller (business logic)
// services/userService.js - Contains business rules and validation
```

### Performance Optimization

**Query Optimization:**
```javascript
// Use indexes on frequently queried columns
// CREATE INDEX idx_user_email ON users(email);

// Limit result sets
const [rows] = await pool.execute(
    'SELECT * FROM users LIMIT ? OFFSET ?',
    [limit, offset]
);

// Use specific columns instead of *
const [rows] = await pool.execute(
    'SELECT id, name, email FROM users'
);
```

### Security Measures

**Environment Variables:**
```javascript
// Never hardcode database credentials
const dbConfig = {
    host: process.env.DB_HOST,
    user: process.env.DB_USER,
    password: process.env.DB_PASSWORD,
    database: process.env.DB_NAME
};
```

**Input Sanitization:**
```javascript
// Always validate and sanitize input
const { body, validationResult } = require('express-validator');

const validateInput = [
    body('email').isEmail().normalizeEmail(),
    body('name').trim().escape(),
    // ... more validation rules
];
```

### Error Handling

**Centralized Error Handling:**
```javascript
// middleware/errorHandler.js
const errorHandler = (error, req, res, next) => {
    console.error('Error:', error);
    
    if (error.code === 'ER_DUP_ENTRY') {
        return res.status(409).json({ error: 'Duplicate entry' });
    }
    
    if (error.code === 'ER_NO_REFERENCED_ROW_2') {
        return res.status(400).json({ error: 'Invalid reference' });
    }
    
    res.status(500).json({ error: 'Internal server error' });
};

module.exports = errorHandler;
```

---

## Summary

### What We Learned:
- **mysql2 package** provides modern MySQL integration
- **Connection pooling** improves performance and reliability
- **CRUD operations** are fundamental database operations
- **Prepared statements** prevent SQL injection and improve performance
- **Transactions** ensure data consistency
- **REST APIs** provide standardized database access
- **Best practices** ensure security and maintainability

### Key Analogies:
- **Connection Pooling** = Team of workers ready for tasks
- **Prepared Statements** = Letter templates with blanks to fill
- **Transactions** = Bank transfers requiring both operations to succeed
- **REST APIs** = Standardized interface for database access
- **Error Handling** = Safety nets for when things go wrong

### Next Steps:
In the next chapter, we'll build a **real-life e-commerce database project** using all these concepts!

---

## Practice Questions

1. What are the benefits of using mysql2 over the mysql package?
2. Why is connection pooling important in Node.js applications?
3. How do prepared statements prevent SQL injection attacks?
4. When would you use transactions in a database application?
5. What's the difference between a connection and a connection pool?
6. How do you handle database errors in a Node.js application?
7. What are the main security considerations when working with MySQL in Node.js?
8. How do you implement pagination in a REST API with MySQL?
9. What's the purpose of environment variables in database configuration?
10. How do you organize code following the MVC pattern with MySQL?

---

**Ready for Chapter 7? Let's build a real-life e-commerce database project!**

# Chapter 7: Real-Life Project: E-commerce Database

## Table of Contents
- [Project Overview](#project-overview)
- [Database Schema Design](#database-schema-design)
- [Setting Up the Project](#setting-up-the-project)
- [Database Implementation](#database-implementation)
- [API Development](#api-development)
- [Advanced Features](#advanced-features)
- [Testing and Deployment](#testing-and-deployment)
- [Project Summary](#project-summary)

---

## Project Overview

**Definition:**
We'll build a complete e-commerce database system with user management, product catalog, shopping cart, order processing, and payment tracking.

### Project Features

**Core Features:**
- **User Management:** Registration, authentication, profiles
- **Product Catalog:** Categories, products, inventory
- **Shopping Cart:** Add/remove items, quantity management
- **Order Processing:** Checkout, order history, status tracking
- **Payment System:** Payment methods, transaction history
- **Admin Panel:** Product management, order management

**Real-World Example:**
Like building a mini Amazon or eBay - a complete online store with all the essential features.

### Project Goals

**Learning Objectives:**
- Apply all MySQL concepts learned
- Build a real-world database application
- Implement proper security and error handling
- Create a scalable and maintainable system

---

## Database Schema Design

**Definition:**
The database schema defines the structure of our e-commerce system with all necessary tables and relationships.

### Entity Relationship Diagram

**Complete E-commerce Schema:**
```
┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│   Users     │         │   Orders    │         │  Products   │
├─────────────┤         ├─────────────┤         ├─────────────┤
│ id (PK)     │         │ id (PK)     │         │ id (PK)     │
│ name        │         │ user_id (FK)│         │ name        │
│ email       │         │ total       │         │ description │
│ password    │         │ status      │         │ price       │
│ role        │         │ created_at  │         │ stock       │
│ created_at  │         └─────────────┘         │ category_id │
└─────────────┘                 │               └─────────────┘
        │                       │                       │
        │                       │                       │
        └─────────── 1:N ───────┘                       │
                                    ┌─────────────┐     │
                                    │Order_Items  │     │
                                    ├─────────────┤     │
                                    │order_id (FK)│─────┘
                                    │product_id(FK)│
                                    │quantity     │
                                    │price        │
                                    └─────────────┘
                                            │
                                            │
                                    ┌─────────────┐
                                    │ Categories  │
                                    ├─────────────┤
                                    │ id (PK)     │
                                    │ name        │
                                    │ description │
                                    └─────────────┘
```

### Database Tables

**Users Table:**
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('user', 'admin') DEFAULT 'user',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

**Categories Table:**
```sql
CREATE TABLE categories (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Products Table:**
```sql
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(200) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    stock INT DEFAULT 0,
    category_id INT,
    image_url VARCHAR(500),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id)
);
```

**Orders Table:**
```sql
CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    total DECIMAL(10,2) NOT NULL,
    status ENUM('pending', 'processing', 'shipped', 'delivered', 'cancelled') DEFAULT 'pending',
    shipping_address TEXT,
    payment_method VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

**Order Items Table:**
```sql
CREATE TABLE order_items (
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

---

## Setting Up the Project

**Definition:**
Setting up the project structure and installing necessary dependencies.

### Project Structure

**Complete Project Layout:**
```
ecommerce-app/
├── config/
│   ├── database.js
│   └── config.js
├── controllers/
│   ├── userController.js
│   ├── productController.js
│   ├── orderController.js
│   └── cartController.js
├── routes/
│   ├── users.js
│   ├── products.js
│   ├── orders.js
│   └── cart.js
├── middleware/
│   ├── auth.js
│   ├── validation.js
│   └── errorHandler.js
├── utils/
│   ├── helpers.js
│   └── constants.js
├── database/
│   ├── schema.sql
│   └── seed.sql
├── .env
├── app.js
└── package.json
```

### Package Installation

**Required Dependencies:**
```bash
# Initialize project
npm init -y

# Install dependencies
npm install express mysql2 dotenv bcryptjs jsonwebtoken cors helmet express-rate-limit express-validator

# Install development dependencies
npm install --save-dev nodemon
```

**Package.json Scripts:**
```json
{
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "db:setup": "mysql -u root -p < database/schema.sql",
    "db:seed": "mysql -u root -p < database/seed.sql"
  }
}
```

### Environment Configuration

**Environment Variables (.env):**
```env
# Server Configuration
PORT=3000
NODE_ENV=development

# Database Configuration
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=ecommerce_db
DB_PORT=3306

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key
JWT_EXPIRES_IN=24h

# Security
BCRYPT_ROUNDS=12
RATE_LIMIT_WINDOW=15
RATE_LIMIT_MAX=100
```

---

## Database Implementation

**Definition:**
Creating the database schema and implementing the database connection.

### Database Schema Creation

**Complete Schema (database/schema.sql):**
```sql
-- Create database
CREATE DATABASE IF NOT EXISTS ecommerce_db;
USE ecommerce_db;

-- Users table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    role ENUM('user', 'admin') DEFAULT 'user',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    INDEX idx_email (email),
    INDEX idx_role (role)
);

-- Categories table
CREATE TABLE categories (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_name (name)
);

-- Products table
CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(200) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    stock INT DEFAULT 0,
    category_id INT,
    image_url VARCHAR(500),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(id) ON DELETE SET NULL,
    INDEX idx_category (category_id),
    INDEX idx_price (price),
    INDEX idx_stock (stock)
);

-- Orders table
CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    total DECIMAL(10,2) NOT NULL,
    status ENUM('pending', 'processing', 'shipped', 'delivered', 'cancelled') DEFAULT 'pending',
    shipping_address TEXT,
    payment_method VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    INDEX idx_user (user_id),
    INDEX idx_status (status),
    INDEX idx_created_at (created_at)
);

-- Order items table
CREATE TABLE order_items (
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES orders(id) ON DELETE CASCADE,
    FOREIGN KEY (product_id) REFERENCES products(id) ON DELETE CASCADE,
    INDEX idx_order (order_id),
    INDEX idx_product (product_id)
);
```

### Database Connection Setup

**Database Configuration (config/database.js):**
```javascript
const mysql = require('mysql2/promise');
require('dotenv').config();

const dbConfig = {
    host: process.env.DB_HOST,
    user: process.env.DB_USER,
    password: process.env.DB_PASSWORD,
    database: process.env.DB_NAME,
    port: process.env.DB_PORT,
    
    // Pool configuration
    connectionLimit: 10,
    acquireTimeout: 60000,
    timeout: 60000,
    reconnect: true,
    waitForConnections: true,
    queueLimit: 0,
    
    // Additional options
    charset: 'utf8mb4',
    timezone: '+00:00'
};

const pool = mysql.createPool(dbConfig);

// Test connection
pool.getConnection()
    .then(connection => {
        console.log('✅ Database connected successfully!');
        connection.release();
    })
    .catch(error => {
        console.error('❌ Database connection failed:', error.message);
    });

module.exports = pool;
```

### Sample Data Seeding

**Seed Data (database/seed.sql):**
```sql
USE ecommerce_db;

-- Insert categories
INSERT INTO categories (name, description) VALUES
('Electronics', 'Electronic devices and gadgets'),
('Clothing', 'Fashion and apparel'),
('Books', 'Books and publications'),
('Home & Garden', 'Home improvement and garden supplies');

-- Insert products
INSERT INTO products (name, description, price, stock, category_id) VALUES
('iPhone 13', 'Latest smartphone from Apple', 999.99, 50, 1),
('Samsung Galaxy S21', 'Android smartphone', 799.99, 30, 1),
('Nike Running Shoes', 'Comfortable running shoes', 89.99, 100, 2),
('Adidas T-Shirt', 'Cotton sports t-shirt', 29.99, 200, 2),
('The Great Gatsby', 'Classic novel by F. Scott Fitzgerald', 12.99, 75, 3),
('Garden Hose', '50ft garden hose', 39.99, 25, 4);

-- Insert admin user (password: admin123)
INSERT INTO users (name, email, password, role) VALUES
('Admin User', 'admin@example.com', '$2b$12$LQv3c1yqBWVHxkd0LHAkCOYz6TtxMQJqhN8/LewdBPj4J/HS.iK2', 'admin');
```

---

## API Development

**Definition:**
Building RESTful APIs for all e-commerce functionality.

### Main Application Setup

**Express App (app.js):**
```javascript
const express = require('express');
const cors = require('cors');
const helmet = require('helmet');
const rateLimit = require('express-rate-limit');
require('dotenv').config();

const userRoutes = require('./routes/users');
const productRoutes = require('./routes/products');
const orderRoutes = require('./routes/orders');
const cartRoutes = require('./routes/cart');
const errorHandler = require('./middleware/errorHandler');

const app = express();
const PORT = process.env.PORT || 3000;

// Security middleware
app.use(helmet());
app.use(cors());

// Rate limiting
const limiter = rateLimit({
    windowMs: process.env.RATE_LIMIT_WINDOW * 60 * 1000,
    max: process.env.RATE_LIMIT_MAX
});
app.use(limiter);

// Body parsing middleware
app.use(express.json({ limit: '10mb' }));
app.use(express.urlencoded({ extended: true }));

// Routes
app.use('/api/users', userRoutes);
app.use('/api/products', productRoutes);
app.use('/api/orders', orderRoutes);
app.use('/api/cart', cartRoutes);

// Health check
app.get('/health', (req, res) => {
    res.json({ status: 'OK', timestamp: new Date().toISOString() });
});

// Error handling middleware
app.use(errorHandler);

// 404 handler
app.use('*', (req, res) => {
    res.status(404).json({ error: 'Route not found' });
});

app.listen(PORT, () => {
    console.log(`🚀 Server running on port ${PORT}`);
    console.log(`📅 Started at: ${new Date().toLocaleString()}`);
});
```

### User Controller

**User Management (controllers/userController.js):**
```javascript
const pool = require('../config/database');
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');

class UserController {
    // Register new user
    async register(userData) {
        const { name, email, password } = userData;
        
        try {
            // Check if user already exists
            const [existingUsers] = await pool.execute(
                'SELECT id FROM users WHERE email = ?',
                [email]
            );
            
            if (existingUsers.length > 0) {
                throw new Error('User already exists');
            }
            
            // Hash password
            const hashedPassword = await bcrypt.hash(password, 12);
            
            // Create user
            const [result] = await pool.execute(
                'INSERT INTO users (name, email, password) VALUES (?, ?, ?)',
                [name, email, hashedPassword]
            );
            
            return {
                id: result.insertId,
                name,
                email,
                message: 'User registered successfully'
            };
        } catch (error) {
            throw error;
        }
    }
    
    // Login user
    async login(credentials) {
        const { email, password } = credentials;
        
        try {
            // Find user
            const [users] = await pool.execute(
                'SELECT * FROM users WHERE email = ?',
                [email]
            );
            
            if (users.length === 0) {
                throw new Error('Invalid credentials');
            }
            
            const user = users[0];
            
            // Check password
            const isPasswordValid = await bcrypt.compare(password, user.password);
            if (!isPasswordValid) {
                throw new Error('Invalid credentials');
            }
            
            // Generate JWT token
            const token = jwt.sign(
                { userId: user.id, email: user.email, role: user.role },
                process.env.JWT_SECRET,
                { expiresIn: process.env.JWT_EXPIRES_IN }
            );
            
            return {
                token,
                user: {
                    id: user.id,
                    name: user.name,
                    email: user.email,
                    role: user.role
                }
            };
        } catch (error) {
            throw error;
        }
    }
    
    // Get user profile
    async getProfile(userId) {
        try {
            const [users] = await pool.execute(
                'SELECT id, name, email, role, created_at FROM users WHERE id = ?',
                [userId]
            );
            
            return users.length > 0 ? users[0] : null;
        } catch (error) {
            throw error;
        }
    }
    
    // Update user profile
    async updateProfile(userId, updateData) {
        const { name, email } = updateData;
        
        try {
            const [result] = await pool.execute(
                'UPDATE users SET name = ?, email = ? WHERE id = ?',
                [name, email, userId]
            );
            
            if (result.affectedRows === 0) {
                throw new Error('User not found');
            }
            
            return { message: 'Profile updated successfully' };
        } catch (error) {
            throw error;
        }
    }
}

module.exports = new UserController();
```

### Product Controller

**Product Management (controllers/productController.js):**
```javascript
const pool = require('../config/database');

class ProductController {
    // Get all products with pagination and filters
    async getProducts(filters = {}) {
        const { 
            page = 1, 
            limit = 10, 
            category, 
            search, 
            minPrice, 
            maxPrice,
            sortBy = 'created_at',
            sortOrder = 'DESC'
        } = filters;
        
        const offset = (page - 1) * limit;
        
        try {
            let query = `
                SELECT p.*, c.name as category_name 
                FROM products p 
                LEFT JOIN categories c ON p.category_id = c.id 
                WHERE 1=1
            `;
            const params = [];
            
            // Add filters
            if (category) {
                query += ' AND p.category_id = ?';
                params.push(category);
            }
            
            if (search) {
                query += ' AND (p.name LIKE ? OR p.description LIKE ?)';
                params.push(`%${search}%`, `%${search}%`);
            }
            
            if (minPrice) {
                query += ' AND p.price >= ?';
                params.push(minPrice);
            }
            
            if (maxPrice) {
                query += ' AND p.price <= ?';
                params.push(maxPrice);
            }
            
            // Add sorting and pagination
            query += ` ORDER BY p.${sortBy} ${sortOrder} LIMIT ? OFFSET ?`;
            params.push(parseInt(limit), offset);
            
            const [products] = await pool.execute(query, params);
            
            // Get total count for pagination
            let countQuery = 'SELECT COUNT(*) as total FROM products WHERE 1=1';
            const countParams = [];
            
            if (category) {
                countQuery += ' AND category_id = ?';
                countParams.push(category);
            }
            
            if (search) {
                countQuery += ' AND (name LIKE ? OR description LIKE ?)';
                countParams.push(`%${search}%`, `%${search}%`);
            }
            
            if (minPrice) {
                countQuery += ' AND price >= ?';
                countParams.push(minPrice);
            }
            
            if (maxPrice) {
                countQuery += ' AND price <= ?';
                countParams.push(maxPrice);
            }
            
            const [countResult] = await pool.execute(countQuery, countParams);
            const total = countResult[0].total;
            
            return {
                products,
                pagination: {
                    page: parseInt(page),
                    limit: parseInt(limit),
                    total,
                    pages: Math.ceil(total / limit)
                }
            };
        } catch (error) {
            throw error;
        }
    }
    
    // Get product by ID
    async getProductById(id) {
        try {
            const [products] = await pool.execute(`
                SELECT p.*, c.name as category_name 
                FROM products p 
                LEFT JOIN categories c ON p.category_id = c.id 
                WHERE p.id = ?
            `, [id]);
            
            return products.length > 0 ? products[0] : null;
        } catch (error) {
            throw error;
        }
    }
    
    // Create product (admin only)
    async createProduct(productData) {
        const { name, description, price, stock, category_id, image_url } = productData;
        
        try {
            const [result] = await pool.execute(
                'INSERT INTO products (name, description, price, stock, category_id, image_url) VALUES (?, ?, ?, ?, ?, ?)',
                [name, description, price, stock, category_id, image_url]
            );
            
            return {
                id: result.insertId,
                name,
                description,
                price,
                stock,
                category_id,
                image_url,
                message: 'Product created successfully'
            };
        } catch (error) {
            throw error;
        }
    }
    
    // Update product (admin only)
    async updateProduct(id, updateData) {
        const { name, description, price, stock, category_id, image_url } = updateData;
        
        try {
            const [result] = await pool.execute(
                'UPDATE products SET name = ?, description = ?, price = ?, stock = ?, category_id = ?, image_url = ? WHERE id = ?',
                [name, description, price, stock, category_id, image_url, id]
            );
            
            if (result.affectedRows === 0) {
                throw new Error('Product not found');
            }
            
            return { message: 'Product updated successfully' };
        } catch (error) {
            throw error;
        }
    }
    
    // Delete product (admin only)
    async deleteProduct(id) {
        try {
            const [result] = await pool.execute(
                'DELETE FROM products WHERE id = ?',
                [id]
            );
            
            if (result.affectedRows === 0) {
                throw new Error('Product not found');
            }
            
            return { message: 'Product deleted successfully' };
        } catch (error) {
            throw error;
        }
    }
}

module.exports = new ProductController();
```

---

## Advanced Features

**Definition:**
Implementing advanced e-commerce features like shopping cart, order processing, and payment integration.

### Shopping Cart Implementation

**Cart Controller (controllers/cartController.js):**
```javascript
const pool = require('../config/database');

class CartController {
    // Add item to cart (session-based)
    async addToCart(userId, productId, quantity) {
        const connection = await pool.getConnection();
        
        try {
            await connection.beginTransaction();
            
            // Check product availability
            const [products] = await connection.execute(
                'SELECT * FROM products WHERE id = ? AND stock >= ?',
                [productId, quantity]
            );
            
            if (products.length === 0) {
                throw new Error('Product not available in requested quantity');
            }
            
            const product = products[0];
            
            // Check if item already in cart
            const [existingItems] = await connection.execute(
                'SELECT * FROM cart WHERE user_id = ? AND product_id = ?',
                [userId, productId]
            );
            
            if (existingItems.length > 0) {
                // Update quantity
                const newQuantity = existingItems[0].quantity + quantity;
                await connection.execute(
                    'UPDATE cart SET quantity = ? WHERE user_id = ? AND product_id = ?',
                    [newQuantity, userId, productId]
                );
            } else {
                // Add new item
                await connection.execute(
                    'INSERT INTO cart (user_id, product_id, quantity, price) VALUES (?, ?, ?, ?)',
                    [userId, productId, quantity, product.price]
                );
            }
            
            await connection.commit();
            return { message: 'Item added to cart successfully' };
            
        } catch (error) {
            await connection.rollback();
            throw error;
        } finally {
            connection.release();
        }
    }
    
    // Get cart items
    async getCart(userId) {
        try {
            const [items] = await pool.execute(`
                SELECT c.*, p.name, p.image_url, p.stock as available_stock
                FROM cart c
                JOIN products p ON c.product_id = p.id
                WHERE c.user_id = ?
            `, [userId]);
            
            let total = 0;
            const cartItems = items.map(item => {
                const itemTotal = item.quantity * item.price;
                total += itemTotal;
                return {
                    ...item,
                    item_total: itemTotal
                };
            });
            
            return {
                items: cartItems,
                total: total
            };
        } catch (error) {
            throw error;
        }
    }
    
    // Update cart item quantity
    async updateCartItem(userId, productId, quantity) {
        try {
            if (quantity <= 0) {
                // Remove item if quantity is 0 or negative
                await this.removeFromCart(userId, productId);
                return { message: 'Item removed from cart' };
            }
            
            const [result] = await pool.execute(
                'UPDATE cart SET quantity = ? WHERE user_id = ? AND product_id = ?',
                [quantity, userId, productId]
            );
            
            if (result.affectedRows === 0) {
                throw new Error('Cart item not found');
            }
            
            return { message: 'Cart updated successfully' };
        } catch (error) {
            throw error;
        }
    }
    
    // Remove item from cart
    async removeFromCart(userId, productId) {
        try {
            const [result] = await pool.execute(
                'DELETE FROM cart WHERE user_id = ? AND product_id = ?',
                [userId, productId]
            );
            
            if (result.affectedRows === 0) {
                throw new Error('Cart item not found');
            }
            
            return { message: 'Item removed from cart' };
        } catch (error) {
            throw error;
        }
    }
    
    // Clear cart
    async clearCart(userId) {
        try {
            await pool.execute(
                'DELETE FROM cart WHERE user_id = ?',
                [userId]
            );
            
            return { message: 'Cart cleared successfully' };
        } catch (error) {
            throw error;
        }
    }
}

module.exports = new CartController();
```

### Order Processing

**Order Controller (controllers/orderController.js):**
```javascript
const pool = require('../config/database');

class OrderController {
    // Create order from cart
    async createOrder(userId, orderData) {
        const connection = await pool.getConnection();
        
        try {
            await connection.beginTransaction();
            
            // Get cart items
            const [cartItems] = await connection.execute(`
                SELECT c.*, p.name, p.stock as available_stock
                FROM cart c
                JOIN products p ON c.product_id = p.id
                WHERE c.user_id = ?
            `, [userId]);
            
            if (cartItems.length === 0) {
                throw new Error('Cart is empty');
            }
            
            // Calculate total and validate stock
            let total = 0;
            for (const item of cartItems) {
                if (item.quantity > item.available_stock) {
                    throw new Error(`Insufficient stock for ${item.name}`);
                }
                total += item.quantity * item.price;
            }
            
            // Create order
            const [orderResult] = await connection.execute(
                'INSERT INTO orders (user_id, total, shipping_address, payment_method) VALUES (?, ?, ?, ?)',
                [userId, total, orderData.shipping_address, orderData.payment_method]
            );
            
            const orderId = orderResult.insertId;
            
            // Create order items and update stock
            for (const item of cartItems) {
                await connection.execute(
                    'INSERT INTO order_items (order_id, product_id, quantity, price) VALUES (?, ?, ?, ?)',
                    [orderId, item.product_id, item.quantity, item.price]
                );
                
                // Update product stock
                await connection.execute(
                    'UPDATE products SET stock = stock - ? WHERE id = ?',
                    [item.quantity, item.product_id]
                );
            }
            
            // Clear cart
            await connection.execute(
                'DELETE FROM cart WHERE user_id = ?',
                [userId]
            );
            
            await connection.commit();
            
            return {
                orderId,
                total,
                message: 'Order created successfully'
            };
            
        } catch (error) {
            await connection.rollback();
            throw error;
        } finally {
            connection.release();
        }
    }
    
    // Get user orders
    async getUserOrders(userId, page = 1, limit = 10) {
        const offset = (page - 1) * limit;
        
        try {
            const [orders] = await pool.execute(`
                SELECT o.*, 
                       COUNT(oi.id) as item_count
                FROM orders o
                LEFT JOIN order_items oi ON o.id = oi.order_id
                WHERE o.user_id = ?
                GROUP BY o.id
                ORDER BY o.created_at DESC
                LIMIT ? OFFSET ?
            `, [userId, limit, offset]);
            
            // Get total count
            const [countResult] = await pool.execute(
                'SELECT COUNT(*) as total FROM orders WHERE user_id = ?',
                [userId]
            );
            
            return {
                orders,
                pagination: {
                    page: parseInt(page),
                    limit: parseInt(limit),
                    total: countResult[0].total,
                    pages: Math.ceil(countResult[0].total / limit)
                }
            };
        } catch (error) {
            throw error;
        }
    }
    
    // Get order details
    async getOrderDetails(orderId, userId) {
        try {
            // Get order
            const [orders] = await pool.execute(
                'SELECT * FROM orders WHERE id = ? AND user_id = ?',
                [orderId, userId]
            );
            
            if (orders.length === 0) {
                throw new Error('Order not found');
            }
            
            const order = orders[0];
            
            // Get order items
            const [items] = await pool.execute(`
                SELECT oi.*, p.name, p.image_url
                FROM order_items oi
                JOIN products p ON oi.product_id = p.id
                WHERE oi.order_id = ?
            `, [orderId]);
            
            return {
                order,
                items
            };
        } catch (error) {
            throw error;
        }
    }
    
    // Update order status (admin only)
    async updateOrderStatus(orderId, status) {
        try {
            const [result] = await pool.execute(
                'UPDATE orders SET status = ? WHERE id = ?',
                [status, orderId]
            );
            
            if (result.affectedRows === 0) {
                throw new Error('Order not found');
            }
            
            return { message: 'Order status updated successfully' };
        } catch (error) {
            throw error;
        }
    }
    
    // Get all orders (admin only)
    async getAllOrders(filters = {}) {
        const { page = 1, limit = 10, status, userId } = filters;
        const offset = (page - 1) * limit;
        
        try {
            let query = `
                SELECT o.*, u.name as user_name, u.email,
                       COUNT(oi.id) as item_count
                FROM orders o
                JOIN users u ON o.user_id = u.id
                LEFT JOIN order_items oi ON o.id = oi.order_id
                WHERE 1=1
            `;
            const params = [];
            
            if (status) {
                query += ' AND o.status = ?';
                params.push(status);
            }
            
            if (userId) {
                query += ' AND o.user_id = ?';
                params.push(userId);
            }
            
            query += ' GROUP BY o.id ORDER BY o.created_at DESC LIMIT ? OFFSET ?';
            params.push(limit, offset);
            
            const [orders] = await pool.execute(query, params);
            
            // Get total count
            let countQuery = 'SELECT COUNT(*) as total FROM orders WHERE 1=1';
            const countParams = [];
            
            if (status) {
                countQuery += ' AND status = ?';
                countParams.push(status);
            }
            
            if (userId) {
                countQuery += ' AND user_id = ?';
                countParams.push(userId);
            }
            
            const [countResult] = await pool.execute(countQuery, countParams);
            
            return {
                orders,
                pagination: {
                    page: parseInt(page),
                    limit: parseInt(limit),
                    total: countResult[0].total,
                    pages: Math.ceil(countResult[0].total / limit)
                }
            };
        } catch (error) {
            throw error;
        }
    }
}

module.exports = new OrderController();
```

---

## Testing and Deployment

**Definition:**
Testing the application and preparing it for deployment.

### API Testing

**Testing with Postman:**
```javascript
// Test user registration
POST /api/users/register
{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123"
}

// Test user login
POST /api/users/login
{
    "email": "john@example.com",
    "password": "password123"
}

// Test product listing
GET /api/products?page=1&limit=10&category=1

// Test adding to cart
POST /api/cart/add
Authorization: Bearer <token>
{
    "productId": 1,
    "quantity": 2
}

// Test creating order
POST /api/orders
Authorization: Bearer <token>
{
    "shipping_address": "123 Main St, City, State 12345",
    "payment_method": "credit_card"
}
```

### Error Handling

**Comprehensive Error Handler (middleware/errorHandler.js):**
```javascript
const errorHandler = (error, req, res, next) => {
    console.error('Error:', error);
    
    // Database errors
    if (error.code === 'ER_DUP_ENTRY') {
        return res.status(409).json({ 
            error: 'Duplicate entry',
            message: 'A record with this information already exists'
        });
    }
    
    if (error.code === 'ER_NO_REFERENCED_ROW_2') {
        return res.status(400).json({ 
            error: 'Invalid reference',
            message: 'Referenced record does not exist'
        });
    }
    
    if (error.code === 'ER_ROW_IS_REFERENCED_2') {
        return res.status(400).json({ 
            error: 'Cannot delete',
            message: 'This record is referenced by other records'
        });
    }
    
    // Validation errors
    if (error.name === 'ValidationError') {
        return res.status(400).json({ 
            error: 'Validation error',
            message: error.message
        });
    }
    
    // JWT errors
    if (error.name === 'JsonWebTokenError') {
        return res.status(401).json({ 
            error: 'Invalid token',
            message: 'Please provide a valid authentication token'
        });
    }
    
    if (error.name === 'TokenExpiredError') {
        return res.status(401).json({ 
            error: 'Token expired',
            message: 'Your session has expired. Please login again'
        });
    }
    
    // Default error
    res.status(500).json({ 
        error: 'Internal server error',
        message: process.env.NODE_ENV === 'development' ? error.message : 'Something went wrong'
    });
};

module.exports = errorHandler;
```

### Deployment Preparation

**Production Configuration:**
```javascript
// config/config.js
const config = {
    development: {
        port: process.env.PORT || 3000,
        database: {
            host: process.env.DB_HOST || 'localhost',
            user: process.env.DB_USER || 'root',
            password: process.env.DB_PASSWORD,
            database: process.env.DB_NAME || 'ecommerce_db',
            port: process.env.DB_PORT || 3306
        },
        jwt: {
            secret: process.env.JWT_SECRET || 'dev_secret',
            expiresIn: process.env.JWT_EXPIRES_IN || '24h'
        }
    },
    production: {
        port: process.env.PORT || 3000,
        database: {
            host: process.env.DB_HOST,
            user: process.env.DB_USER,
            password: process.env.DB_PASSWORD,
            database: process.env.DB_NAME,
            port: process.env.DB_PORT || 3306
        },
        jwt: {
            secret: process.env.JWT_SECRET,
            expiresIn: process.env.JWT_EXPIRES_IN || '24h'
        }
    }
};

const env = process.env.NODE_ENV || 'development';
module.exports = config[env];
```

---

## Project Summary

**Definition:**
A complete summary of what we've built and learned.

### What We Built

**Complete E-commerce System:**
- **User Management:** Registration, authentication, profiles
- **Product Catalog:** Categories, products, search, filtering
- **Shopping Cart:** Add/remove items, quantity management
- **Order Processing:** Checkout, order history, status tracking
- **Admin Features:** Product management, order management
- **Security:** JWT authentication, input validation, SQL injection prevention

### Key Features Implemented

**Database Features:**
- Proper normalization and relationships
- Indexes for performance optimization
- Transactions for data consistency
- Prepared statements for security

**API Features:**
- RESTful API design
- Pagination and filtering
- Error handling and validation
- Authentication and authorization

**Security Features:**
- Password hashing with bcrypt
- JWT token authentication
- Input validation and sanitization
- SQL injection prevention
- Rate limiting

### Learning Outcomes

**Technical Skills:**
- MySQL database design and implementation
- Node.js and Express.js development
- RESTful API development
- Security best practices
- Error handling and debugging

**Real-World Application:**
- Building a complete business application
- Managing complex data relationships
- Implementing user authentication
- Handling concurrent users and transactions

---

## Summary

### What We Learned:
- **Complete e-commerce system** with all essential features
- **Database design** with proper relationships and constraints
- **RESTful API development** with Express.js and MySQL
- **Security implementation** with authentication and validation
- **Transaction management** for data consistency
- **Error handling** and debugging techniques

### Key Analogies:
- **E-commerce System** = Digital store with inventory and customers
- **Database Design** = Blueprint for organizing store data
- **API Development** = Store clerk handling customer requests
- **Security** = Store security system protecting data
- **Transactions** = Cash register ensuring accurate sales

### Next Steps:
In the final chapter, we'll explore **advanced MySQL concepts and best practices** for production applications!

---

## Practice Questions

1. What are the main tables in the e-commerce database and their relationships?
2. How do you implement user authentication in the e-commerce system?
3. What security measures are implemented in the project?
4. How does the shopping cart functionality work?
5. What is the order processing flow in the system?
6. How do you handle concurrent users and data consistency?
7. What are the benefits of using transactions in order processing?
8. How do you implement pagination and filtering in the product API?
9. What error handling strategies are used in the application?
10. How would you scale this e-commerce system for production use?

---

**Ready for Chapter 8? Let's explore advanced MySQL concepts and best practices!**

# Chapter 8: Advanced MySQL Concepts and Best Practices

## Table of Contents
- [Performance Optimization](#performance-optimization)
- [Advanced Indexing Strategies](#advanced-indexing-strategies)
- [Query Optimization](#query-optimization)
- [Database Backup and Recovery](#database-backup-and-recovery)
- [Replication and High Availability](#replication-and-high-availability)
- [Security Best Practices](#security-best-practices)
- [Monitoring and Maintenance](#monitoring-and-maintenance)
- [Scaling Strategies](#scaling-strategies)
- [Final Project: Complete Implementation](#final-project-complete-implementation)

---

## Performance Optimization

**Definition:**
Performance optimization involves tuning MySQL to handle more requests faster while using fewer resources.

### MySQL Configuration Optimization

**Key Configuration Parameters:**
```ini
[mysqld]
# Buffer pool size (70-80% of available RAM)
innodb_buffer_pool_size = 1G

# Log file size
innodb_log_file_size = 256M

# Query cache (if using MyISAM)
query_cache_size = 64M
query_cache_type = 1

# Connection settings
max_connections = 200
max_connect_errors = 1000

# Table cache
table_open_cache = 2000

# Thread cache
thread_cache_size = 8

# Sort buffer
sort_buffer_size = 2M
read_buffer_size = 2M
read_rnd_buffer_size = 8M
```

**Real-World Example:**
Like tuning a car engine - you adjust various settings to get the best performance for your specific needs.

### Memory Management

**Buffer Pool Optimization:**
```sql
-- Check buffer pool usage
SHOW ENGINE INNODB STATUS;

-- Monitor buffer pool efficiency
SELECT 
    (SELECT COUNT(*) FROM information_schema.tables WHERE table_schema = 'your_database') as tables,
    (SELECT COUNT(*) FROM information_schema.tables WHERE table_schema = 'your_database' AND engine = 'InnoDB') as innodb_tables;
```

**Real-World Example:**
Like managing RAM in your computer - you want to keep frequently used data in fast memory.

---

## Advanced Indexing Strategies

**Definition:**
Advanced indexing strategies help optimize query performance for complex scenarios.

### Composite Indexes

**Multi-Column Indexes:**
```sql
-- Create composite index for common query patterns
CREATE INDEX idx_user_status_created ON users (status, created_at);

-- This index helps with queries like:
SELECT * FROM users WHERE status = 'active' ORDER BY created_at DESC;
SELECT * FROM users WHERE status = 'active' AND created_at > '2023-01-01';
```

**Index Order Matters:**
```sql
-- Good: Most selective column first
CREATE INDEX idx_email_status ON users (email, status);

-- Bad: Less selective column first
CREATE INDEX idx_status_email ON users (status, email);
```

**Real-World Example:**
Like organizing a library by both author and then title - you can quickly find books by a specific author, or by author and title together.

### Partial Indexes

**Indexing Specific Conditions:**
```sql
-- Index only active users
CREATE INDEX idx_active_users ON users (email) WHERE status = 'active';

-- Index only recent orders
CREATE INDEX idx_recent_orders ON orders (user_id, created_at) 
WHERE created_at > DATE_SUB(NOW(), INTERVAL 1 YEAR);
```

### Covering Indexes

**Indexes That Include All Needed Data:**
```sql
-- Covering index for user list
CREATE INDEX idx_user_list ON users (status, created_at, name, email);

-- Query uses only the index (no table lookup needed)
SELECT name, email FROM users WHERE status = 'active' ORDER BY created_at DESC;
```

---

## Query Optimization

**Definition:**
Query optimization involves writing and tuning SQL queries for maximum performance.

### Using EXPLAIN

**Analyzing Query Performance:**
```sql
-- Analyze query execution plan
EXPLAIN SELECT u.name, o.total 
FROM users u 
JOIN orders o ON u.id = o.user_id 
WHERE u.status = 'active' 
ORDER BY o.created_at DESC;

-- EXPLAIN output shows:
-- - Which indexes are used
-- - How many rows are examined
-- - Join types and order
-- - Temporary tables or filesorts
```

**Understanding EXPLAIN Output:**
```sql
-- Good: Using index, few rows examined
EXPLAIN SELECT * FROM users WHERE email = 'john@example.com';
-- type: const, rows: 1

-- Bad: Full table scan
EXPLAIN SELECT * FROM users WHERE name LIKE '%john%';
-- type: ALL, rows: 10000
```

### Query Optimization Techniques

**Avoiding Common Pitfalls:**
```sql
-- ❌ BAD: Using functions on indexed columns
SELECT * FROM users WHERE YEAR(created_at) = 2023;

-- ✅ GOOD: Use range conditions
SELECT * FROM users WHERE created_at >= '2023-01-01' AND created_at < '2024-01-01';

-- ❌ BAD: SELECT * (retrieves unnecessary data)
SELECT * FROM users WHERE status = 'active';

-- ✅ GOOD: Select only needed columns
SELECT id, name, email FROM users WHERE status = 'active';
```

**Optimizing JOINs:**
```sql
-- Use appropriate JOIN types
-- INNER JOIN: Only matching records
SELECT u.name, o.total 
FROM users u 
INNER JOIN orders o ON u.id = o.user_id;

-- LEFT JOIN: All users, even without orders
SELECT u.name, COUNT(o.id) as order_count
FROM users u 
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.name;
```

---

## Database Backup and Recovery

**Definition:**
Backup and recovery strategies ensure data safety and business continuity.

### Backup Types

**Logical Backups:**
```bash
# Export entire database
mysqldump -u root -p --all-databases > full_backup.sql

# Export specific database
mysqldump -u root -p ecommerce_db > ecommerce_backup.sql

# Export with specific options
mysqldump -u root -p \
  --single-transaction \
  --routines \
  --triggers \
  --events \
  ecommerce_db > complete_backup.sql
```

**Physical Backups:**
```bash
# Stop MySQL service
sudo systemctl stop mysql

# Copy data directory
sudo cp -r /var/lib/mysql /backup/mysql_$(date +%Y%m%d)

# Start MySQL service
sudo systemctl start mysql
```

### Automated Backup Script

**Backup Automation:**
```bash
#!/bin/bash
# backup_script.sh

# Configuration
DB_USER="root"
DB_PASS="your_password"
DB_NAME="ecommerce_db"
BACKUP_DIR="/backup/mysql"
DATE=$(date +%Y%m%d_%H%M%S)

# Create backup directory
mkdir -p $BACKUP_DIR

# Create backup
mysqldump -u $DB_USER -p$DB_PASS \
  --single-transaction \
  --routines \
  --triggers \
  $DB_NAME > $BACKUP_DIR/${DB_NAME}_${DATE}.sql

# Compress backup
gzip $BACKUP_DIR/${DB_NAME}_${DATE}.sql

# Keep only last 7 days of backups
find $BACKUP_DIR -name "*.sql.gz" -mtime +7 -delete

echo "Backup completed: ${DB_NAME}_${DATE}.sql.gz"
```

### Recovery Procedures

**Restoring from Backup:**
```bash
# Restore entire database
mysql -u root -p < full_backup.sql

# Restore specific database
mysql -u root -p ecommerce_db < ecommerce_backup.sql

# Restore compressed backup
gunzip -c ecommerce_backup.sql.gz | mysql -u root -p ecommerce_db
```

---

## Replication and High Availability

**Definition:**
Replication creates copies of your database for read scaling, backup, and high availability.

### Master-Slave Replication

**Setting Up Replication:**
```sql
-- On Master Server (my.cnf)
[mysqld]
server-id = 1
log-bin = mysql-bin
binlog_format = ROW
sync_binlog = 1

-- On Slave Server (my.cnf)
[mysqld]
server-id = 2
relay-log = mysql-relay-bin
read_only = 1
```

**Configuring Replication:**
```sql
-- On Master: Create replication user
CREATE USER 'repl'@'%' IDENTIFIED BY 'repl_password';
GRANT REPLICATION SLAVE ON *.* TO 'repl'@'%';

-- Get master status
SHOW MASTER STATUS;

-- On Slave: Configure replication
CHANGE MASTER TO
  MASTER_HOST = 'master_ip',
  MASTER_USER = 'repl',
  MASTER_PASSWORD = 'repl_password',
  MASTER_LOG_FILE = 'mysql-bin.000001',
  MASTER_LOG_POS = 154;

START SLAVE;

-- Check slave status
SHOW SLAVE STATUS\G
```

### Read Scaling

**Load Balancing Reads:**
```javascript
// Application-level read scaling
const masterPool = mysql.createPool({
    host: 'master-server',
    // ... other config
});

const slavePool = mysql.createPool({
    host: 'slave-server',
    // ... other config
});

// Use master for writes, slave for reads
async function getUsers() {
    return await slavePool.execute('SELECT * FROM users');
}

async function createUser(userData) {
    return await masterPool.execute('INSERT INTO users SET ?', userData);
}
```

---

## Security Best Practices

**Definition:**
Security best practices protect your database from unauthorized access and attacks.

### User Management

**Principle of Least Privilege:**
```sql
-- Create application user with minimal privileges
CREATE USER 'app_user'@'%' IDENTIFIED BY 'strong_password';

-- Grant only necessary privileges
GRANT SELECT, INSERT, UPDATE, DELETE ON ecommerce_db.* TO 'app_user'@'%';

-- Create read-only user for reporting
CREATE USER 'report_user'@'%' IDENTIFIED BY 'report_password';
GRANT SELECT ON ecommerce_db.* TO 'report_user'@'%';

-- Create admin user for maintenance
CREATE USER 'admin_user'@'localhost' IDENTIFIED BY 'admin_password';
GRANT ALL PRIVILEGES ON ecommerce_db.* TO 'admin_user'@'localhost';
```

### Network Security

**Securing MySQL Network Access:**
```sql
-- Bind MySQL to specific IP (not 0.0.0.0)
[mysqld]
bind-address = 127.0.0.1

-- Use SSL for remote connections
[mysqld]
ssl-ca = /path/to/ca.pem
ssl-cert = /path/to/server-cert.pem
ssl-key = /path/to/server-key.pem
require_ssl = 1
```

### Data Encryption

**Encrypting Sensitive Data:**
```sql
-- Encrypt sensitive columns
ALTER TABLE users 
ADD COLUMN encrypted_ssn VARBINARY(255);

-- Encrypt data before storing
INSERT INTO users (name, encrypted_ssn) 
VALUES ('John Doe', AES_ENCRYPT('123-45-6789', 'encryption_key'));

-- Decrypt data when retrieving
SELECT name, AES_DECRYPT(encrypted_ssn, 'encryption_key') as ssn 
FROM users;
```

---

## Monitoring and Maintenance

**Definition:**
Regular monitoring and maintenance ensure optimal database performance and health.

### Performance Monitoring

**Key Metrics to Monitor:**
```sql
-- Check slow queries
SHOW VARIABLES LIKE 'slow_query_log';
SHOW VARIABLES LIKE 'long_query_time';

-- Monitor connections
SHOW STATUS LIKE 'Threads_connected';
SHOW STATUS LIKE 'Max_used_connections';

-- Check buffer pool efficiency
SHOW STATUS LIKE 'Innodb_buffer_pool_read_requests';
SHOW STATUS LIKE 'Innodb_buffer_pool_reads';

-- Monitor query cache (if using)
SHOW STATUS LIKE 'Qcache_hits';
SHOW STATUS LIKE 'Qcache_inserts';
```

### Regular Maintenance

**Automated Maintenance Script:**
```sql
-- Analyze tables for better query optimization
ANALYZE TABLE users, orders, products;

-- Optimize tables to reclaim space
OPTIMIZE TABLE users, orders, products;

-- Check table integrity
CHECK TABLE users, orders, products;

-- Repair tables if needed
REPAIR TABLE users, orders, products;
```

**Maintenance Automation:**
```bash
#!/bin/bash
# maintenance_script.sh

DB_USER="root"
DB_PASS="your_password"
DB_NAME="ecommerce_db"

# Connect to MySQL and run maintenance
mysql -u $DB_USER -p$DB_PASS $DB_NAME << EOF
ANALYZE TABLE users, orders, products;
OPTIMIZE TABLE users, orders, products;
CHECK TABLE users, orders, products;
EOF

echo "Maintenance completed at $(date)"
```

---

## Scaling Strategies

**Definition:**
Scaling strategies help your database handle increased load and data volume.

### Vertical Scaling

**Upgrading Server Resources:**
```ini
# Increase buffer pool for more RAM
innodb_buffer_pool_size = 4G

# Increase connection limit
max_connections = 500

# Optimize for SSD storage
innodb_io_capacity = 2000
innodb_io_capacity_max = 4000
```

### Horizontal Scaling

**Database Sharding:**
```sql
-- Shard by user_id (modulo 4)
-- Shard 0: user_id % 4 = 0
-- Shard 1: user_id % 4 = 1
-- Shard 2: user_id % 4 = 2
-- Shard 3: user_id % 4 = 3

-- Application-level sharding logic
function getShard(userId) {
    return userId % 4;
}

function getConnection(userId) {
    const shard = getShard(userId);
    return shardPools[shard];
}
```

**Read Replicas:**
```javascript
// Load balancing across multiple read replicas
const replicaPools = [
    mysql.createPool({ host: 'replica1' }),
    mysql.createPool({ host: 'replica2' }),
    mysql.createPool({ host: 'replica3' })
];

function getReadConnection() {
    // Round-robin or random selection
    const index = Math.floor(Math.random() * replicaPools.length);
    return replicaPools[index];
}
```

---

## Final Project: Complete Implementation

**Definition:**
A complete implementation showcasing all advanced concepts in a production-ready system.

### Production-Ready Configuration

**Complete my.cnf Configuration:**
```ini
[mysqld]
# Basic settings
port = 3306
socket = /var/run/mysqld/mysqld.sock
pid-file = /var/run/mysqld/mysqld.pid

# Character set
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

# InnoDB settings
default-storage-engine = InnoDB
innodb_buffer_pool_size = 1G
innodb_log_file_size = 256M
innodb_log_buffer_size = 16M
innodb_flush_log_at_trx_commit = 1
innodb_lock_wait_timeout = 50

# Connection settings
max_connections = 200
max_connect_errors = 1000
connect_timeout = 10
wait_timeout = 28800
interactive_timeout = 28800

# Query cache
query_cache_type = 1
query_cache_size = 64M
query_cache_limit = 2M

# Buffer settings
sort_buffer_size = 2M
read_buffer_size = 2M
read_rnd_buffer_size = 8M
myisam_sort_buffer_size = 8M

# Logging
slow_query_log = 1
slow_query_log_file = /var/log/mysql/slow.log
long_query_time = 2
log_error = /var/log/mysql/error.log

# Security
local_infile = 0
sql_mode = STRICT_TRANS_TABLES,NO_ZERO_DATE,NO_ZERO_IN_DATE,ERROR_FOR_DIVISION_BY_ZERO
```

### Monitoring Dashboard

**Performance Monitoring Script:**
```javascript
// monitoring.js
const mysql = require('mysql2/promise');
const fs = require('fs');

class DatabaseMonitor {
    constructor(config) {
        this.pool = mysql.createPool(config);
    }

    async getPerformanceMetrics() {
        const metrics = {};
        
        // Connection metrics
        const [connections] = await this.pool.execute('SHOW STATUS LIKE "Threads_connected"');
        metrics.activeConnections = connections[0].Value;
        
        // Buffer pool metrics
        const [bufferPool] = await this.pool.execute('SHOW STATUS LIKE "Innodb_buffer_pool_read_requests"');
        metrics.bufferPoolReads = bufferPool[0].Value;
        
        // Slow query count
        const [slowQueries] = await this.pool.execute('SHOW STATUS LIKE "Slow_queries"');
        metrics.slowQueries = slowQueries[0].Value;
        
        // Uptime
        const [uptime] = await this.pool.execute('SHOW STATUS LIKE "Uptime"');
        metrics.uptime = uptime[0].Value;
        
        return metrics;
    }

    async logMetrics() {
        const metrics = await this.getPerformanceMetrics();
        const logEntry = {
            timestamp: new Date().toISOString(),
            ...metrics
        };
        
        fs.appendFileSync('/var/log/mysql/metrics.log', JSON.stringify(logEntry) + '\n');
    }
}

// Usage
const monitor = new DatabaseMonitor({
    host: 'localhost',
    user: 'monitor_user',
    password: 'monitor_password',
    database: 'mysql'
});

// Log metrics every 5 minutes
setInterval(() => {
    monitor.logMetrics();
}, 5 * 60 * 1000);
```

### Backup and Recovery Automation

**Complete Backup System:**
```bash
#!/bin/bash
# complete_backup_system.sh

# Configuration
DB_USER="backup_user"
DB_PASS="backup_password"
DB_NAME="ecommerce_db"
BACKUP_DIR="/backup/mysql"
LOG_FILE="/var/log/mysql/backup.log"
RETENTION_DAYS=30

# Functions
log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> $LOG_FILE
}

# Create backup
log "Starting backup process"
mkdir -p $BACKUP_DIR

# Full backup
mysqldump -u $DB_USER -p$DB_PASS \
    --single-transaction \
    --routines \
    --triggers \
    --events \
    --hex-blob \
    --add-drop-database \
    --databases $DB_NAME > $BACKUP_DIR/full_backup_$(date +%Y%m%d_%H%M%S).sql

if [ $? -eq 0 ]; then
    log "Full backup completed successfully"
    
    # Compress backup
    gzip $BACKUP_DIR/full_backup_$(date +%Y%m%d_%H%M%S).sql
    
    # Clean old backups
    find $BACKUP_DIR -name "*.sql.gz" -mtime +$RETENTION_DAYS -delete
    log "Old backups cleaned"
else
    log "Backup failed!"
    exit 1
fi

# Verify backup
if [ -f $BACKUP_DIR/full_backup_$(date +%Y%m%d_%H%M%S).sql.gz ]; then
    log "Backup verification successful"
else
    log "Backup verification failed"
    exit 1
fi

log "Backup process completed"
```

---

## Summary

### What We Learned:
- **Performance optimization** through configuration and indexing
- **Advanced indexing strategies** for complex queries
- **Query optimization** using EXPLAIN and best practices
- **Backup and recovery** procedures for data safety
- **Replication** for high availability and read scaling
- **Security best practices** for production environments
- **Monitoring and maintenance** for ongoing health
- **Scaling strategies** for growth

### Key Analogies:
- **Performance Optimization** = Tuning a car engine for maximum efficiency
- **Indexing Strategies** = Creating multiple filing systems for different access patterns
- **Query Optimization** = Planning the fastest route to your destination
- **Backup and Recovery** = Insurance policy for your data
- **Replication** = Creating backup copies that stay synchronized
- **Security** = Installing locks and alarms on your data vault
- **Monitoring** = Dashboard showing your system's vital signs
- **Scaling** = Adding more lanes to a highway as traffic increases

### Congratulations!
You've completed the comprehensive MySQL Database Guide! You now have the knowledge and skills to:
- Design and implement robust database systems
- Build secure and performant applications
- Handle real-world database challenges
- Scale your applications for growth
- Maintain and optimize production databases

---

## Final Practice Questions

1. How do you determine the optimal buffer pool size for your MySQL server?
2. What are the benefits of composite indexes and when should you use them?
3. How do you use EXPLAIN to optimize a slow query?
4. What are the different types of MySQL backups and when should you use each?
5. How do you set up master-slave replication for high availability?
6. What security measures should you implement in a production MySQL environment?
7. How do you monitor MySQL performance and what metrics are most important?
8. What are the differences between vertical and horizontal scaling?
9. How do you implement database sharding for horizontal scaling?
10. What maintenance tasks should be automated in a production environment?

---

**🎉 Congratulations! You've mastered MySQL Database Development! 🎉**

You're now ready to build robust, scalable, and secure database applications. Keep practicing, stay updated with the latest MySQL features, and continue building amazing applications!

**Happy Coding! 🚀**
