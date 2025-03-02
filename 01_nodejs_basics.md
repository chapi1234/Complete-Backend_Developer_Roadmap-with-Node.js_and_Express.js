# Node.js Basics

## Introduction to Node.js

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It allows you to run JavaScript on the server-side.

## Node.js Installation and Setup

To install Node.js, download the installer from the [official website](https://nodejs.org/) and follow the installation instructions.

Verify the installation:

```bash
node -v
npm -v
```

## Understanding the Event Loop

The event loop is the mechanism that allows Node.js to perform non-blocking I/O operations.

## Global Objects and Modules

Node.js provides several global objects, such as `__dirname`, `__filename`, `require`, and `module`.

Example:

```javascript
console.log(__dirname); // Prints the directory name of the current module
console.log(__filename); // Prints the file name of the current module
```

## File System Operations

Node.js provides the `fs` module to interact with the file system.

Example:

```javascript
const fs = require("fs");

// Reading a file
fs.readFile("example.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Writing to a file
fs.writeFile("example.txt", "Hello, world!", (err) => {
  if (err) throw err;
  console.log("File written successfully");
});
```
