# Advanced Express.js

## Advanced Routing Techniques

Example:

```javascript
const express = require("express");
const app = express();
const port = 3000;

const router = express.Router();

router.get("/user/:id", (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});

app.use("/api", router);

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## Using Templating Engines

### EJS

```bash
npm install ejs
```

Example:

```javascript
const express = require("express");
const app = express();
const port = 3000;

app.set("view engine", "ejs");

app.get("/", (req, res) => {
  res.render("index", { title: "EJS Example" });
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

### Pug

```bash
npm install pug
```

Example:

```javascript
const express = require("express");
const app = express();
const port = 3000;

app.set("view engine", "pug");

app.get("/", (req, res) => {
  res.render("index", { title: "Pug Example" });
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## Building RESTful APIs

Example:

```javascript
const express = require("express");
const app = express();
const port = 3000;

app.use(express.json());

app.get("/api/users", (req, res) => {
  res.send("Get all users");
});

app.post("/api/users", (req, res) => {
  res.send("Create a user");
});

app.get("/api/users/:id", (req, res) => {
  res.send(`Get user with ID: ${req.params.id}`);
});

app.put("/api/users/:id", (req, res) => {
  res.send(`Update user with ID: ${req.params.id}`);
});

app.delete("/api/users/:id", (req, res) => {
  res.send(`Delete user with ID: ${req.params.id}`);
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## Versioning APIs

Example:

```javascript
const express = require("express");
const app = express();
const port = 3000;

app.use(express.json());

const v1 = express.Router();
const v2 = express.Router();

v1.get("/users", (req, res) => {
  res.send("Get all users - v1");
});

v2.get("/users", (req, res) => {
  res.send("Get all users - v2");
});

app.use("/api/v1", v1);
app.use("/api/v2", v2);

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```
