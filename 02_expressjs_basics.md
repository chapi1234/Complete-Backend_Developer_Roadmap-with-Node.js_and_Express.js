# Express.js Basics

## Introduction to Express.js

Express.js is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications.

## Setting Up an Express.js Application

To set up an Express.js application, you need to install the Express package using npm.

```bash
npm install express
```

Create a basic Express.js application:

```javascript
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello, World!");
});

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

## Middleware Functions

Middleware functions are functions that have access to the request object, the response object, and the next middleware function in the application’s request-response cycle.

Example:

```javascript
app.use((req, res, next) => {
  console.log("Middleware function");
  next();
});
```

## Routing

Routing refers to how an application’s endpoints (URIs) respond to client requests.

Example:

```javascript
app.get("/about", (req, res) => {
  res.send("About Page");
});
```

## Handling Requests and Responses

Express provides methods to handle HTTP requests and responses.

Example:

```javascript
app.post("/submit", (req, res) => {
  res.send("Form Submitted");
});
```
