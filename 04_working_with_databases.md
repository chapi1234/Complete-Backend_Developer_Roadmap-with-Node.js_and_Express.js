# Working with Databases

## Connecting to Databases

### MongoDB

To connect to MongoDB, you need to install the `mongodb` package.

```bash
npm install mongodb
```

Example:

```javascript
const { MongoClient } = require("mongodb");
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);

async function run() {
  try {
    await client.connect();
    console.log("Connected to MongoDB");
  } finally {
    await client.close();
  }
}

run().catch(console.dir);
```

### MySQL

To connect to MySQL, you need to install the `mysql` package.

```bash
npm install mysql
```

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
  console.log("Connected to MySQL");
});
```

## CRUD Operations

### MongoDB

Example:

```javascript
const { MongoClient } = require("mongodb");
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);

async function run() {
  try {
    await client.connect();
    const database = client.db("test");
    const collection = database.collection("documents");

    // Create
    await collection.insertOne({ name: "John Doe" });

    // Read
    const document = await collection.findOne({ name: "John Doe" });
    console.log(document);

    // Update
    await collection.updateOne(
      { name: "John Doe" },
      { $set: { name: "Jane Doe" } }
    );

    // Delete
    await collection.deleteOne({ name: "Jane Doe" });
  } finally {
    await client.close();
  }
}

run().catch(console.dir);
```

### MySQL

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

  // Create
  connection.query(
    'INSERT INTO users (name) VALUES ("John Doe")',
    (err, result) => {
      if (err) throw err;
      console.log("User inserted");

      // Read
      connection.query(
        'SELECT * FROM users WHERE name = "John Doe"',
        (err, result) => {
          if (err) throw err;
          console.log(result);

          // Update
          connection.query(
            'UPDATE users SET name = "Jane Doe" WHERE name = "John Doe"',
            (err, result) => {
              if (err) throw err;
              console.log("User updated");

              // Delete
              connection.query(
                'DELETE FROM users WHERE name = "Jane Doe"',
                (err, result) => {
                  if (err) throw err;
                  console.log("User deleted");
                  connection.end();
                }
              );
            }
          );
        }
      );
    }
  );
});
```

## Using ORMs

### Mongoose (MongoDB)

```bash
npm install mongoose
```

Example:

```javascript
const mongoose = require("mongoose");
mongoose.connect("mongodb://localhost:27017/test", {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

const userSchema = new mongoose.Schema({
  name: String,
});

const User = mongoose.model("User", userSchema);

// Create
const user = new User({ name: "John Doe" });
user.save().then(() => console.log("User saved"));

// Read
User.findOne({ name: "John Doe" }).then((user) => console.log(user));

// Update
User.updateOne({ name: "John Doe" }, { name: "Jane Doe" }).then(() =>
  console.log("User updated")
);

// Delete
User.deleteOne({ name: "Jane Doe" }).then(() => console.log("User deleted"));
```

### Sequelize (MySQL)

```bash
npm install sequelize mysql2
```

Example:

```javascript
const { Sequelize, DataTypes } = require("sequelize");
const sequelize = new Sequelize("test", "root", "", {
  host: "localhost",
  dialect: "mysql",
});

const User = sequelize.define(
  "User",
  {
    name: {
      type: DataTypes.STRING,
      allowNull: false,
    },
  },
  {}
);

sequelize.sync().then(() => {
  // Create
  User.create({ name: "John Doe" }).then(() => console.log("User created"));

  // Read
  User.findOne({ where: { name: "John Doe" } }).then((user) =>
    console.log(user)
  );

  // Update
  User.update({ name: "Jane Doe" }, { where: { name: "John Doe" } }).then(() =>
    console.log("User updated")
  );

  // Delete
  User.destroy({ where: { name: "Jane Doe" } }).then(() =>
    console.log("User deleted")
  );
});
```
