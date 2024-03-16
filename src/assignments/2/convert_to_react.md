# Convert your HTML and CSS project into React

## Step 1: Set Up Your React Environment

Make sure you have Node.js installed on your system.
Use Create React App to set up your project. Run the following command in your terminal:

```bash
npx create-react-app todo-app
```

Navigate into the project directory:

```bash
cd todo-app
```

Start the development server:

```bash
npm start
```

## Step 2: Create Components

Inside the src folder, create a new folder named components.
Create a new file named Todo.js inside the components folder.
Open Todo.js and create a functional component for Todo items.

## Step 3: Define State and Event Handlers

In the src folder, open App.js.
Define state to manage the list of Todo items.
Write event handlers to add, delete, and toggle Todo items.

## Step 4: Render Todo List

Inside the render method of App.js, map through the list of Todo items and render each Todo component.
Pass necessary props (e.g., Todo text, completion status) to the Todo component.

## Step 5: Implement Add Todo Functionality

Create an input field and a button in the App component for adding new Todo items.
Write a function to handle adding new Todo items to the list.

## Step 6: Implement Delete and Toggle Functionality

Add delete and toggle buttons to each Todo item component.
Write functions to handle deleting and toggling Todo items.

## Step 7: Styling

Use CSS to style your Todo App components.
Make it visually appealing by adding colors, fonts, and layout adjustments.

## Extra Features

* Local Storage: Implement local storage to persist Todo items between page refreshes.
* Filtering: Add filtering options to filter Todo items based on completion status (e.g., all, active, completed).
* Edit Todo: Allow users to edit existing Todo items.
* Clear Completed: Add a button to clear all completed Todo items from the list.
* Multiple Lists: Allow users to create multiple Todo lists/categories.
* Drag and Drop: Implement drag and drop functionality to reorder Todo items.
* Themes: Allow users to choose from different themes for the Todo App.

## Example code for the Todo App in React, along with additional features like local storage and filtering

### Todo.js Component

```jsx
import React from 'react';

const Todo = ({ todo, toggleTodo, deleteTodo }) => {
  return (
    <div className={`todo ${todo.completed ? 'completed' : ''}`}>
      <input
        type="checkbox"
        checked={todo.completed}
        onChange={() => toggleTodo(todo.id)}
      />
      <p>{todo.text}</p>
      <button onClick={() => deleteTodo(todo.id)}>Delete</button>
    </div>
  );
};

export default Todo;
```

### App.js Component

```jsx
import React, { useState, useEffect } from 'react';
import Todo from './components/Todo';
import './App.css';

const App = () => {
  const [todos, setTodos] = useState([]);
  const [newTodo, setNewTodo] = useState('');

  useEffect(() => {
    const storedTodos = JSON.parse(localStorage.getItem('todos'));
    if (storedTodos) {
      setTodos(storedTodos);
    }
  }, []);

  useEffect(() => {
    localStorage.setItem('todos', JSON.stringify(todos));
  }, [todos]);

  const addTodo = () => {
    if (newTodo.trim() === '') return;
    const newTodoItem = {
      id: Date.now(),
      text: newTodo,
      completed: false,
    };
    setTodos([...todos, newTodoItem]);
    setNewTodo('');
  };

  const toggleTodo = (id) => {
    const updatedTodos = todos.map((todo) =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    );
    setTodos(updatedTodos);
  };

  const deleteTodo = (id) => {
    const updatedTodos = todos.filter((todo) => todo.id !== id);
    setTodos(updatedTodos);
  };

  return (
    <div className="App">
      <h1>Todo App</h1>
      <input
        type="text"
        value={newTodo}
        onChange={(e) => setNewTodo(e.target.value)}
        placeholder="Add new todo..."
      />
      <button onClick={addTodo}>Add Todo</button>
      <div className="todo-list">
        {todos.map((todo) => (
          <Todo
            key={todo.id}
            todo={todo}
            toggleTodo={toggleTodo}
            deleteTodo={deleteTodo}
          />
        ))}
      </div>
    </div>
  );
};

export default App;
```

### App.css

```css
.App {
  text-align: center;
  margin-top: 50px;
}

.todo {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.todo.completed {
  text-decoration: line-through;
}

input[type='checkbox'] {
  margin-right: 10px;
}

.todo-list {
  margin-top: 20px;
}

button {
  margin-left: 10px;
}
```
