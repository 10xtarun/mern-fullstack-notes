# Drill Down Props from Parent to Child in ReactJS

## Introduction

In this project, we will create a simple React application to demonstrate the concept of passing props from a parent component to a child component, and then drilling down those props to even deeper child components. This is a fundamental concept in React and is essential for building scalable and reusable components.

## Steps

### Step 1: Create Parent and Child Components

Inside the src folder, create a new file named ParentComponent.js.
Create a functional component named ParentComponent in ParentComponent.js.
Create another file named ChildComponent.js.
Create a functional component named ChildComponent in ChildComponent.js.

### Step 3: Pass Props from Parent to Child

In ParentComponent.js, define some props (e.g., name, age).
Render the ChildComponent inside ParentComponent and pass the props to it.
In ChildComponent.js, receive the props and render them or pass them down further to deeper child components if needed.

### Step 3: Display Props in Child Component

In ChildComponent.js, receive the props passed from the parent component.
Display the received props in the JSX of the ChildComponent.

Example Code:

ParentComponent.js:

```jsx
import React from 'react';
import ChildComponent from './ChildComponent';

const ParentComponent = () => {
  return (
    <div>
      <h1>Parent Component</h1>
      <ChildComponent name="John" age={30} />
    </div>
  );
};

export default ParentComponent;
```

ChildComponent.js:

```jsx
import React from 'react';

const ChildComponent = (props) => {
  return (
    <div>
      <h2>Child Component</h2>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
    </div>
  );
};

export default ChildComponent;
```

App.js (Main Component):

```jsx
import React from 'react';
import ParentComponent from './ParentComponent';

const App = () => {
  return (
    <div className="App">
      <ParentComponent />
    </div>
  );
};

export default App;
```

## Future Additions

1. Nested Child Components: Add more levels of child components to demonstrate deeper drilling of props.
2. Dynamic Props: Pass dynamic props from parent to child components based on user input or state changes.
3. Event Handling: Pass down event handler functions as props to child components.
4. Context API: Replace props drilling with React Context API for managing global state.
5. Component Composition: Use component composition techniques to compose complex UI components from smaller, reusable components.

---
