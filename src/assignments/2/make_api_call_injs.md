# Make API Calls and Show User Details

## Introduction

In this project, we will create a simple web application that makes API calls to fetch user details from a public API and displays them on the webpage. We'll use HTML, CSS, and JavaScript to build the frontend of the application.

## Prerequisites

Basic knowledge of HTML, CSS, and JavaScript.
Access to a public API that provides user data (e.g., JSONPlaceholder).

## Project Overview

We'll build a single-page web application with the following features:

* Input field to enter the user ID.
* Button to trigger the API call.
* Display area to show the user details fetched from the API.

## Steps to Build the Project

### Step 1: Set Up Your Project

Create a new folder for your project and set up the basic structure with the following files:

1. index.html: Main HTML file.
2. styles.css: CSS stylesheet for styling.
3. script.js: JavaScript file for handling API calls and DOM manipulation.

### Step 2: Design the Layout

Define the layout of your web application using HTML. Use semantic HTML elements to structure different sections of the webpage, such as `<header>, <main>, <section>, and <footer>`. Add input fields, buttons, and display areas as needed.

### Step 3: Style Your Web Application

Apply CSS styles to make your web application visually appealing. Use CSS for layout, typography, colors, and spacing. You can create custom styles or use CSS frameworks like Bootstrap or Bulma for pre-designed components and layouts.

### Step 4: Make API Calls

Write JavaScript code to make API calls to fetch user details from the public API. You can use the fetch() function or libraries like Axios to make HTTP requests. Parse the response data (usually in JSON format) and extract the relevant user details.

### Step 5: Display User Details

Update the DOM dynamically with the user details fetched from the API. Use JavaScript to manipulate the DOM and display the user details in the designated display area on the webpage.

### Step 6: Test and Refine

Test your web application by entering different user IDs and verifying that the user details are fetched and displayed correctly. Make any necessary adjustments to improve the user experience and responsiveness of the application.

Example Code:

HTML (index.html):

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Details</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>User Details</h1>
    </header>
    <main>
        <section>
            <label for="userId">Enter User ID:</label>
            <input type="text" id="userId" placeholder="Enter user ID...">
            <button onclick="fetchUserDetails()">Get Details</button>
        </section>
        <section id="userDetails">
            <!-- User details will be displayed here -->
        </section>
    </main>
    <footer>
        <p>&copy; 2023 User Details. All rights reserved.</p>
    </footer>
    <script src="script.js"></script>
</body>
</html>
```

CSS (styles.css):

```css
/* Reset styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
    background-color: #f4f4f4;
}

header {
    background: #333;
    color: #fff;
    padding: 20px;
    text-align: center;
}

main {
    padding: 20px;
}

section {
    margin-bottom: 20px;
}

input[type="text"] {
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    width: 200px;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    background-color: #333;
    color: #fff;
    border: none;
}

button:hover {
    background-color: #555;
}

#userDetails {
    background: #fff;
    padding: 20px;
}
```

JavaScript (script.js):

```js
function fetchUserDetails() {
    const userId = document.getElementById('userId').value;

    fetch(`https://jsonplaceholder.typicode.com/users/${userId}`)
        .then(response => response.json())
        .then(user => {
            displayUserDetails(user);
        })
        .catch(error => {
            console.error('Error fetching user details:', error);
        });
}

function displayUserDetails(user) {
    const userDetailsSection = document.getElementById('userDetails');

    userDetailsSection.innerHTML = `
        <h2>User Details</h2>
        <p><strong>Name:</strong> ${user.name}</p
```

---
