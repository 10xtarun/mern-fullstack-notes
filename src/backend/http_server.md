# Modules: http (server)

Creating a basic server in Node.js using the http module involves a few simple steps. We'll focus on handling GET and POST requests without performing any specific operations, just to demonstrate how to set up the server and handle these requests.

Step 1: Import the http Module
First, you need to import the http module, which is a built-in module in Node.js for creating HTTP servers.

```js
const http = require('http');
```

Step 2: Create the Server
Next, you create the server using the http.createServer() method. This method takes a callback function as an argument, which is called whenever a request is received by the server. The callback function itself takes two arguments: a request object (req) and a response object (res).

```js
const server = http.createServer((req, res) => {
    // Handle the request here
});
```

Step 3: Handle GET Requests
Inside the callback function, you can check the request method to determine if it's a GET request. If it is, you can send a response back to the client.

```js
if (req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello, this is a GET request!\n');
}
```

Step 4: Handle POST Requests
Similarly, you can check for POST requests and handle them accordingly. For simplicity, we'll just acknowledge the POST request without performing any operations on the data sent.

```js
if (req.method === 'POST') {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello, this is a POST request!\n');
}
```

Step 5: Start the Server
Finally, you need to start the server by calling the listen() method on the server object. This method takes a port number as an argument and optionally a hostname.

```js
const port = 3000;
server.listen(port, () => {
    console.log(`Server running at http://localhost:${port}/`);
});
```

Complete Example
Here's the complete code for a basic server that handles GET and POST requests:

```js
const http = require('http');

const server = http.createServer((req, res) => {
    if (req.method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello, this is a GET request!\n');
    } else if (req.method === 'POST') {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello, this is a POST request!\n');
    }
});

const port = 3000;
server.listen(port, () => {
    console.log(`Server running at http://localhost:${port}/`);
});
```

### Explanation
* Importing the http Module: This is the first step where you make the http module available in your script.
* Creating the Server: You create a server that listens for incoming requests. The callback function is where you define how to handle these requests.
* Handling GET and POST Requests: Inside the callback, you check the request method. If it's a GET request, you send a simple response. If it's a POST request, you send a different response.
* Starting the Server: Finally, you start the server on a specific port. Once the server is running, it listens for incoming requests and handles them based on the logic you've defined.

> This basic server setup is a starting point for building more complex applications in Node.js.

---
