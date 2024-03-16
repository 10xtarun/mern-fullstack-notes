# Fetch Data using an API in ReactJS

## Introduction

In this project, we will create a simple React application to demonstrate how to fetch data from an API and display it on the webpage. We'll use the fetch API or Axios library to make HTTP requests to a public API, and then render the fetched data in our React components.

## Project Overview

We'll build a React application that fetches and displays data from a public API. We'll use functional components and React hooks to manage state and lifecycle methods.

## Step 1: Create Components

Inside the src folder, create a new file named UserList.js.
Create a functional component named UserList in UserList.js.
This component will be responsible for fetching and displaying the list of users from the API.

## Step 2: Fetch Data from API

Use the fetch API or Axios library to make an HTTP GET request to a public API (e.g., JSONPlaceholder).
Retrieve the list of users from the API response and store it in the component's state using React hooks (e.g., useState).

## Step 3: Display Data in Component

Render the list of users fetched from the API in the UserList component.
Use JSX to map through the list of users and display each user's information (e.g., name, email) in the UI.

Example Code:

UserList.js:

```jsx
import React, { useState, useEffect } from 'react';

const UserList = () => {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then((response) => response.json())
      .then((data) => setUsers(data))
      .catch((error) => console.error('Error fetching users:', error));
  }, []);

  return (
    <div>
      <h1>User List</h1>
      <ul>
        {users.map((user) => (
          <li key={user.id}>
            <p>Name: {user.name}</p>
            <p>Email: {user.email}</p>
          </li>
        ))}
      </ul>
    </div>
  );
};

export default UserList;
```

App.js (Main Component):

```jsx
import React from 'react';
import UserList from './UserList';

const App = () => {
  return (
    <div className="App">
      <UserList />
    </div>
  );
};

export default App;
```

## Future Additions

1. Loading Spinner: Add a loading spinner while data is being fetched from the API.
2. Error Handling: Implement error handling to display a friendly message if the API request fails.
3. Pagination: Add pagination to handle large datasets and improve performance.
4. Search Functionality: Implement a search bar to filter users based on criteria.
5. Sorting: Allow users to sort the user list based on different attributes (e.g., name, email).
Caching: Implement caching to avoid unnecessary API calls and improve performance.

---
