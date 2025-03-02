# Asynchronous Programming

## Callbacks

Callbacks are functions passed as arguments to other functions and executed after some operation has been completed.

Example:

```javascript
function fetchData(callback) {
  setTimeout(() => {
    callback("Data fetched");
  }, 1000);
}

fetchData((data) => {
  console.log(data);
});
```

## Promises

Promises represent the eventual completion (or failure) of an asynchronous operation and its resulting value.

Example:

```javascript
const fetchData = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Data fetched");
  }, 1000);
});

fetchData.then((data) => {
  console.log(data);
});
```

## Async/Await

Async/Await is syntactic sugar built on top of promises, making asynchronous code look and behave more like synchronous code.

Example:

```javascript
async function fetchData() {
  const data = await new Promise((resolve) => {
    setTimeout(() => {
      resolve("Data fetched");
    }, 1000);
  });
  console.log(data);
}

fetchData();
```
