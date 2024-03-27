# REST API: http (server)

## What is REST Concept/Architecture?

> REST, which stands for Representational State Transfer, is a set of architectural principles for designing networked applications. It's a way to structure your application so that it can be easily understood and used by other applications. In simple terms, REST is like a set of rules for how different parts of a web application should talk to each other.

### Key Concepts of REST:

1. Resources: In REST, everything is a resource. A resource can be anything that can be named and addressed, such as a document, an image, a temporal service, a collection of other resources, a non-virtual object, and so on. In the context of a web application, resources are often represented by URLs.

2. HTTP Methods: REST uses standard HTTP methods to perform operations on resources. The most common methods are GET (retrieve a resource), POST (create a new resource), PUT (update an existing resource), and DELETE (remove a resource).

3. Stateless: Each request from a client to a server must contain all the information needed to understand and process the request. The server should not store anything about the latest HTTP request the client made. Each request is processed independently.

4. Client-Server Architecture: The client is responsible for the user interface and user experience, and the server is responsible for processing requests and managing resources. The client and server communicate over HTTP, and they can be developed independently as long as they adhere to the same interface.

5. Cacheable: Responses from the server can be cached by the client. This can improve performance by reducing the need for repeated requests for the same data.

## Adding Resources/URLs to the Server created in previous page

To demonstrate REST principles, let's add a simple resource to our server. We'll create a resource named "message" that can be accessed via a URL.

Step 1: Define the Resource URL
We'll use the URL path /message to represent our "message" resource.

Step 2: Update the Server to Handle the Resource
We'll modify the server to handle GET and POST requests specifically for the /message resource.

```js
const http = require('http');

const server = http.createServer((req, res) => {
    const url = req.url;

    if (req.method === 'GET' && url === '/message') {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('This is the GET response for the /message resource.\n');
    } else if (req.method === 'POST' && url === '/message') {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('This is the POST response for the /message resource.\n');
    } else {
        res.writeHead(404, { 'Content-Type': 'text/plain' });
        res.end('Not Found\n');
    }
});

const port = 3000;
server.listen(port, () => {
    console.log(`Server running at http://localhost:${port}/`);
});
```

### Explanation

1. Resource URL: We've defined /message as the URL for our "message" resource. This is how clients will access this resource.

2. Handling GET and POST Requests: The server checks if the request is for the /message resource and if it's a GET or POST request. It then sends a response specific to the request method.

3. 404 Response: If the request is not for the /message resource or if it's not a GET or POST request, the server sends a 404 Not Found response.

> This simple example demonstrates how to structure a server to follow REST principles by defining resources and handling them with specific HTTP methods.

---
