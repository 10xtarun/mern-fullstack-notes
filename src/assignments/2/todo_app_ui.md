# Todo App UI using HTML and CSS

## Overview

In this project, we will create a simple Todo App User Interface (UI) using HTML and CSS. The Todo App will allow users to add tasks, mark tasks as completed, and delete tasks. We'll focus on creating a clean and intuitive interface that is easy to use.

## Steps

### Setup

Create a new folder for your project and create two files: index.html and styles.css.

### HTML Structure

Open index.html and set up the basic structure of the Todo App UI using HTML tags. Here's a simple example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Todo App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Todo App</h1>
        <div class="todo-list">
            <input type="text" placeholder="Add a new task">
            <button>Add Task</button>
            <ul>
                <!-- Todo tasks will be dynamically added here -->
            </ul>
        </div>
    </div>
</body>
</html>
```

### CSS Styling

Open styles.css and add CSS rules to style the Todo App UI. Here's an example to get started:

```css
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
}

.container {
    max-width: 600px;
    margin: 20px auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

h1 {
    text-align: center;
}

.todo-list {
    margin-top: 20px;
}

input[type="text"] {
    width: 70%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-right: 10px;
}

button {
    padding: 10px 20px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    background-color: #f9f9f9;
    padding: 10px;
    margin-top: 10px;
    border-radius: 5px;
}

li.completed {
    text-decoration: line-through;
    background-color: #d3d3d3;
}

.delete-btn {
    background-color: #dc3545;
    color: #fff;
    border: none;
    padding: 5px 10px;
    border-radius: 3px;
    cursor: pointer;
    margin-left: 5px;
}
```

### Functionality

Add JavaScript to make the Todo App interactive (optional). You can add functionality to add tasks, mark tasks as completed, and delete tasks using JavaScript.

This example demonstrates a basic Todo App UI with an input field to add tasks, a button to add tasks, and a list to display tasks. Each task has a delete button, and completed tasks are crossed out for visual indication.

Feel free to customize and enhance the Todo App UI according to your preferences and requirements. Happy coding!

---
