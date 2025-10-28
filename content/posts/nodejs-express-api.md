---
title: "Building RESTful APIs with Node.js and Express"
date: 2024-01-10T14:30:00+00:00
draft: false
description: "Learn how to create robust RESTful APIs using Node.js and Express framework"
tags: ["Node.js", "Express", "API", "Backend", "JavaScript"]
categories: ["Web Development", "Tutorials"]
author: "Alibek Konyrtai"
---

# Building RESTful APIs with Node.js and Express

Creating RESTful APIs is a fundamental skill for backend developers. In this tutorial, we'll build a complete API using Node.js and Express, covering best practices and common patterns.

## Project Setup

First, let's initialize our project:

```bash
mkdir my-api
cd my-api
npm init -y
npm install express cors helmet morgan
npm install -D nodemon
```

## Basic Express Server

Here's a simple Express server setup:

```javascript
const express = require('express');
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');

const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(helmet());
app.use(cors());
app.use(morgan('combined'));
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Routes
app.get('/api/health', (req, res) => {
  res.json({ status: 'OK', timestamp: new Date().toISOString() });
});

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

## RESTful Routes

Let's create a complete CRUD API for a users resource:

```javascript
// In-memory storage (use a database in production)
let users = [
  { id: 1, name: 'John Doe', email: 'john@example.com' },
  { id: 2, name: 'Jane Smith', email: 'jane@example.com' }
];

// GET /api/users
app.get('/api/users', (req, res) => {
  res.json(users);
});

// GET /api/users/:id
app.get('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }
  res.json(user);
});

// POST /api/users
app.post('/api/users', (req, res) => {
  const { name, email } = req.body;
  
  if (!name || !email) {
    return res.status(400).json({ error: 'Name and email are required' });
  }
  
  const newUser = {
    id: users.length + 1,
    name,
    email
  };
  
  users.push(newUser);
  res.status(201).json(newUser);
});

// PUT /api/users/:id
app.put('/api/users/:id', (req, res) => {
  const userIndex = users.findIndex(u => u.id === parseInt(req.params.id));
  
  if (userIndex === -1) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  const { name, email } = req.body;
  users[userIndex] = { ...users[userIndex], name, email };
  
  res.json(users[userIndex]);
});

// DELETE /api/users/:id
app.delete('/api/users/:id', (req, res) => {
  const userIndex = users.findIndex(u => u.id === parseInt(req.params.id));
  
  if (userIndex === -1) {
    return res.status(404).json({ error: 'User not found' });
  }
  
  users.splice(userIndex, 1);
  res.status(204).send();
});
```

## Error Handling

Implement proper error handling middleware:

```javascript
// Error handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ 
    error: 'Something went wrong!',
    message: process.env.NODE_ENV === 'development' ? err.message : 'Internal server error'
  });
});

// 404 handler
app.use('*', (req, res) => {
  res.status(404).json({ error: 'Route not found' });
});
```

## Best Practices

1. **Use environment variables** for configuration
2. **Implement proper validation** for request data
3. **Add authentication and authorization** as needed
4. **Use HTTPS** in production
5. **Implement rate limiting** to prevent abuse
6. **Add comprehensive logging** for debugging

## Conclusion

Building RESTful APIs with Node.js and Express is straightforward once you understand the patterns. Remember to follow REST conventions, implement proper error handling, and always validate your data.

---

*Ready to build your own API? Start with this foundation and expand based on your needs!*
