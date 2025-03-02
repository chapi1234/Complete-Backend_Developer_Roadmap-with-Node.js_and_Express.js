# Security

## Securing Express.js Applications

### Helmet

Helmet helps secure Express.js apps by setting various HTTP headers.

### Installing Dependencies

```bash
npm install helmet
```

### Example

```javascript
const express = require("express");
const helmet = require("helmet");
const app = express();
const port = 3000;

app.use(helmet());

app.get("/", (req, res) => {
  res.send("Hello, World!");
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## Preventing Common Vulnerabilities

### SQL Injection

Use parameterized queries to prevent SQL injection.

Example:

```javascript
const mysql = require("mysql");
const connection = mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "",
  database: "test",
});

connection.connect((err) => {
  if (err) throw err;

  const userId = 1;
  connection.query(
    "SELECT * FROM users WHERE id = ?",
    [userId],
    (err, results) => {
      if (err) throw err;
      console.log(results);
    }
  );
});
```

### Cross-Site Scripting (XSS)

Sanitize user input to prevent XSS attacks.

Example:

```javascript
const express = require("express");
const app = express();
const port = 3000;

app.use(express.json());

app.post("/submit", (req, res) => {
  const userInput = req.body.input;
  const sanitizedInput = userInput.replace(/</g, "&lt;").replace(/>/g, "&gt;");
  res.send(`Sanitized input: ${sanitizedInput}`);
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

### Cross-Site Request Forgery (CSRF)

Use CSRF tokens to prevent CSRF attacks.

### Installing Dependencies

```bash
npm install csurf
```

### Example

```javascript
const express = require("express");
const csurf = require("csurf");
const cookieParser = require("cookie-parser");
const app = express();
const port = 3000;

app.use(cookieParser());
app.use(csurf({ cookie: true }));

app.get("/form", (req, res) => {
  res.send(`<form action="/submit" method="POST">
              <input type="hidden" name="_csrf" value="${req.csrfToken()}">
              <button type="submit">Submit</button>
            </form>`);
});

app.post("/submit", (req, res) => {
  res.send("Form submitted");
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```
