# Modules Fundamentals

## What are modules in NodeJS?

> In Node.js, a module is essentially a JavaScript file that contains code, functions, objects, or values that can be used in other parts of your application. Modules help in organizing code into reusable parts, making it easier to maintain and understand. They also help in managing dependencies and avoiding naming conflicts.

### How Modules Work in Node.js

1. Exporting: A module can export functions, objects, or values that it defines, making them available to other modules. This is done using the module.exports or exports object.

2. Importing: Other modules can import and use the exported members of a module by using the require() function.


## Inbuilt Modules in Node.js

> Node.js comes with a set of built-in modules that provide various functionalities without needing to install any additional packages. These modules are part of the Node.js runtime and can be used directly in your applications. Some of the most commonly used inbuilt modules include:

1. fs (File System): Provides functions to work with the file system, such as reading from and writing to files.

2. http: Allows Node.js to transfer data over the HTTP protocol. It can be used to create HTTP servers and clients.

3. path: Offers utilities for working with file and directory paths.

4. os: Provides information about the operating system, such as the operating system's name, version, and architecture.

5. events: Implements the EventEmitter class, which is used to handle events within Node.js applications.

6. util: Contains utility functions, such as inherits for prototype inheritance and format for string formatting.

7. process: Provides information about, and control over, the current Node.js process. It can be used to read environment variables, exit the process, and more.

8. stream: Provides the foundation for all streaming APIs in Node.js, allowing data to be read from and written to in a non-blocking manner.

## Simplified Explanation of Module:

Imagine you're building a house. Each room (module) in the house has a specific purpose (e.g., kitchen for cooking, bedroom for sleeping). The inbuilt modules in Node.js are like the basic furniture and appliances that come with the house, allowing you to perform essential tasks without needing to buy or build everything from scratch.

In the context of Node.js, these modules are like the basic tools and utilities that come with the Node.js runtime, enabling you to perform common tasks like file operations, network communication, and more, without needing to write all the code from scratch.

---
