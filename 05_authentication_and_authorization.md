# Authentication and Authorization

## User Authentication (JWT)

JSON Web Tokens (JWT) are used for securely transmitting information between parties as a JSON object.

### Installing Dependencies

```bash
npm install jsonwebtoken bcryptjs
```

### Example

```javascript
const express = require("express");
const jwt = require("jsonwebtoken");
const bcrypt = require("bcryptjs");
const app = express();
const port = 3000;

app.use(express.json());

const users = []; // This should be replaced with a database in a real application

app.post("/register", async (req, res) => {
  const { username, password } = req.body;
  const hashedPassword = await bcrypt.hash(password, 10);
  users.push({ username, password: hashedPassword });
  res.status(201).send("User registered");
});

app.post("/login", async (req, res) => {
  const { username, password } = req.body;
  const user = users.find((u) => u.username === username);
  if (user && (await bcrypt.compare(password, user.password))) {
    const token = jwt.sign({ username }, "secret_key", { expiresIn: "1h" });
    res.json({ token });
  } else {
    res.status(401).send("Invalid credentials");
  }
});

app.get("/protected", (req, res) => {
  const token = req.headers["authorization"];
  if (token) {
    jwt.verify(token, "secret_key", (err, decoded) => {
      if (err) {
        res.status(401).send("Invalid token");
      } else {
        res.send("Protected content");
      }
    });
  } else {
    res.status(401).send("No token provided");
  }
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## Role-Based Access Control

Example:

```javascript
const roles = {
  admin: ["read", "write", "delete"],
  user: ["read"],
};

function authorize(role, action) {
  return (req, res, next) => {
    const token = req.headers["authorization"];
    if (token) {
      jwt.verify(token, "secret_key", (err, decoded) => {
        if (err) {
          res.status(401).send("Invalid token");
        } else {
          if (roles[role].includes(action)) {
            next();
          } else {
            res.status(403).send("Forbidden");
          }
        }
      });
    } else {
      res.status(401).send("No token provided");
    }
  };
}

app.get("/admin", authorize("admin", "read"), (req, res) => {
  res.send("Admin content");
});
```
