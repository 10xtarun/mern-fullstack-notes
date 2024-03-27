# Moduel: File System

We will use inbuilt file system module of nodeJS to read file by 2 different techniques:

> Creating file reader functionality in Node.js can be achieved using both callbacks and promises. Let's start by implementing file reading using callbacks and then using promises. We'll use the fs module, which is a built-in module in Node.js for file system operations.

1. Using Callbacks
    * In Node.js, a callback is a function passed as an argument to another function, which is then invoked inside the outer function to complete some kind of routine or action.

* Step 1: Import the fs module

```js
const fs = require('fs');
```

* Step 2: Implement the file reading functionality using a callback

```js
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error reading file:', err);
        return;
    }
    console.log('File content:', data);
});
```

In this example, fs.readFile is used to read the file example.txt. The second argument 'utf8' specifies the encoding. The third argument is a callback function that takes two parameters: err and data. If an error occurs during the file reading process, err will contain the error object, and data will be undefined. If the file is read successfully, err will be null, and data will contain the file content as a string.

2. Using Promises
    * Promises in JavaScript represent the eventual completion (or failure) of an asynchronous operation and its resulting value.

* Step 1: Import the fs module

```js
const fs = require('fs').promises;
```

Note: We're using fs.promises here to work with promises.

* Step 2: Implement the file reading functionality using promises

```js
fs.readFile('example.txt', 'utf8')
    .then(data => {
        console.log('File content:', data);
    })
    .catch(err => {
        console.error('Error reading file:', err);
    });
```

In this example, fs.readFile returns a promise that resolves with the file content if the file is read successfully. We use .then() to handle the resolved value (the file content) and .catch() to handle any errors that occur during the file reading process.

### Differences Between Callbacks and Promises
1. Syntax and Structure: Callbacks are functions passed as arguments to another function, while promises are objects that represent the eventual completion of an asynchronous operation.
2. Error Handling: With callbacks, errors are handled in the callback function itself. With promises, errors are handled in a .catch() block, which makes error handling more consistent and centralized.
3. Chaining: Promises can be chained together using .then(), allowing for more complex asynchronous operations to be performed in a more readable and maintainable way. Callbacks can lead to callback hell when dealing with multiple asynchronous operations.
4. Readability and Maintainability: Promises, with their .then() and .catch() methods, can lead to more readable and maintainable code, especially when dealing with multiple asynchronous operations.
5. Error Propagation: In promises, errors are propagated down the chain until they are caught by a .catch() block. This makes it easier to handle errors in a centralized manner. With callbacks, error handling needs to be done in each callback function, which can lead to repetitive and error-prone code.

> In summary, while both callbacks and promises can be used for asynchronous operations in Node.js, promises offer a more modern, powerful, and readable approach to handling asynchronous operations.

### Following table will give better understanding of asynchronous options in NodeJS

| Feature        | Callbacks                           | Promises                                                |   |   |
|----------------|-------------------------------------|---------------------------------------------------------|---|---|
| Structure      | Nested functions                    | Single Promise object with .then() and .catch() methods |   |   |
| Readability    | Less readable with nested callbacks | More readable and easier to follow                      |   |   |
| Error Handling | Requires manual error checking      | Built-in error handling with .catch()                   |   |   |

---

