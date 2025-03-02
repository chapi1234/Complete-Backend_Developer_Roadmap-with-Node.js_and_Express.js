# Testing

## Unit Testing with Mocha/Chai

Mocha is a feature-rich JavaScript test framework, and Chai is an assertion library.

### Installing Dependencies

```bash
npm install mocha chai --save-dev
```

### Example

```javascript
// test.js
const { expect } = require("chai");

describe("Array", () => {
  it("should return -1 when the value is not present", () => {
    expect([1, 2, 3].indexOf(4)).to.equal(-1);
  });
});
```

### Running Tests

```bash
npx mocha test.js
```

## Integration Testing

Integration testing involves testing multiple components together.

### Example

```javascript
// app.js
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello, World!");
});

if (require.main === module) {
  app.listen(port, () => {
    console.log(`Server running on http://localhost:${port}`);
  });
} else {
  module.exports = app;
}
```

```javascript
// test.js
const request = require("supertest");
const app = require("./app");
const { expect } = require("chai");

describe("GET /", () => {
  it("should return Hello, World!", (done) => {
    request(app)
      .get("/")
      .expect(200)
      .end((err, res) => {
        if (err) return done(err);
        expect(res.text).to.equal("Hello, World!");
        done();
      });
  });
});
```

### Running Tests

```bash
npx mocha test.js
```

## End-to-End Testing

End-to-end testing involves testing the entire application flow.

### Example with Cypress

```bash
npm install cypress --save-dev
```

### Example

```javascript
// cypress/integration/sample_spec.js
describe("My First Test", () => {
  it("Visits the Kitchen Sink", () => {
    cy.visit("https://example.cypress.io");
    cy.contains("type").click();
    cy.url().should("include", "/commands/actions");
    cy.get(".action-email")
      .type("fake@email.com")
      .should("have.value", "fake@email.com");
  });
});
```

### Running Tests

```bash
npx cypress open
```
