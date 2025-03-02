# Error Handling

## Error Handling Middleware

Express provides a way to handle errors using middleware.

Example:

```javascript
const express = require("express");
const app = express();
const port = 3000;

app.use(express.json());

app.get("/", (req, res) => {
  throw new Error("Something went wrong!");
});

// Error handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send("Something broke!");
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## Logging Errors

You can use logging libraries like `winston` to log errors.

### Installing Dependencies

```bash
npm install winston
```

### Example

```javascript
const express = require("express");
const winston = require("winston");
const app = express();
const port = 3000;

const logger = winston.createLogger({
  level: "error",
  format: winston.format.json(),
  transports: [new winston.transports.File({ filename: "error.log" })],
});

app.use(express.json());

app.get("/", (req, res) => {
  throw new Error("Something went wrong!");
});

// Error handling middleware
app.use((err, req, res, next) => {
  logger.error(err.stack);
  res.status(500).send("Something broke!");
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```
