# Exercise: Objects

How can you access a property of an object in JavaScript?
```js
const person = {
  name: 'John',
  age: 30,
  location: 'New York'
};

// accessing a property using dot notation
console.log(person.name); // John

// accessing a property using square bracket notation
console.log(person['age']); // 30
```

In this example, we have an object named person with three properties: name, age, and location. To access a property of an object, we can use dot notation or square bracket notation. Dot notation is used when we know the property name at the time of coding, and square bracket notation is used when the property name is dynamic or when it contains special characters.

---

How can you add a new property to an object in JavaScript?
```js
const person = {
  name: 'John',
  age: 30,
};

// adding a new property using dot notation
person.location = 'New York';

// adding a new property using square bracket notation
person['occupation'] = 'Software Developer';

console.log(person);
// { name: 'John', age: 30, location: 'New York', occupation: 'Software Developer' }
```

In this example, we have an object named person with two properties: name and age. To add a new property to an object, we can use dot notation or square bracket notation. We can assign a value to the new property using the assignment operator.

---

Sorting an array of objects by a specific property: Given an array of objects with various properties, sort the array based on a specific property value. For example, sort an array of objects containing employee data by their salary in descending order.
```js
const employees = [
  { name: 'Alice', salary: 50000 },
  { name: 'Bob', salary: 60000 },
  { name: 'Charlie', salary: 45000 },
  { name: 'Dave', salary: 70000 },
];

employees.sort((a, b) => b.salary - a.salary);

console.log(employees);
// Output: [{ name: 'Dave', salary: 70000 }, { name: 'Bob', salary: 60000 }, { name: 'Alice', salary: 50000 }, { name: 'Charlie', salary: 45000 }]
```

Note: This is not complete solution, think and code.

---

Merging multiple objects into one: Given multiple objects, merge them into a single object with all the properties and values. If a property exists in multiple objects, use the value from the last object that contains that property.

```js
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };
const obj3 = { c: 5, d: 6 };

const merged = Object.assign({}, obj1, obj2, obj3);

console.log(merged);
// Output: { a: 1, b: 3, c: 5, d: 6 }
```

---
