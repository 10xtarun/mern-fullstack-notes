# Objects in JS

> An object is a data type that represents a collection of related data and/or functionality. Objects are used to organize and store data in a structured way.

## Important features of objects in JavaScript:

* Properties: Objects have properties, which are key-value pairs. The key is a string (or symbol), and the value can be any data type, including other objects. Properties are accessed using dot notation or bracket notation.
Example:
```js
let person = {
  name: "John",
  age: 30,
  address: {
    street: "123 Main St",
    city: "Anytown",
    state: "CA"
  }
};

console.log(person.name); // "John"
console.log(person.address.city); // "Anytown"
```

* Methods: Objects can have methods, which are functions that are properties of the object. Methods are accessed using dot notation.
Example:
```js
let person = {
  name: "John",
  age: 30,
  sayHello: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

person.sayHello(); // "Hello, my name is John"
```

* Constructors: Objects can be created using constructor functions, which are functions that are used to create new objects. Constructor functions use the new keyword to create a new instance of the object.
Example:

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.sayHello = function() {
    console.log(`Hello, my name is ${this.name}`);
  };
}

let person1 = new Person("John", 30);
let person2 = new Person("Jane", 25);

console.log(person1.name); // "John"
console.log(person2.age); // 25
person1.sayHello(); // "Hello, my name is John"
```

* Prototypes: Objects can inherit properties and methods from a prototype object, which is a template object that is used to create new objects. Prototypes are accessed using the prototype property of a constructor function.
Example:

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`);
};

let person1 = new Person("John", 30);
let person2 = new Person("Jane", 25);

console.log(person1.name); // "John"
console.log(person2.age); // 25
person1.sayHello(); // "Hello, my name is John"
```

---

## Some common manipulations related to objects in JavaScript include:

1. Adding and deleting properties:

```js
let person = {
  name: "John",
  age: 30
};

person.address = "123 Main St";
delete person.age;

console.log(person); // { name: "John", address: "123 Main St" }
```

2. Looping over properties:

```js
let person = {
  name: "John",
  age: 30
};

for (let prop in person) {
  console.log(`${prop}: ${person[prop]}`);
}

// Output:
// name: John
// age: 30
```

3. Cloning objects:

```js
let person = {
  name: "John",
  age: 30
};

let clone = Object.assign({}, person);

console.log(clone); // { name: "John", age: 30 }
```

---

## Loop / Iterate through JS Objects

There are different ways to loop through JS objects.

1. for...in loop: This loop is used to iterate over the properties of an object.
Example:
```js
let person = {
  name: "John",
  age: 30,
  gender: "male"
};

for (let prop in person) {
  console.log(`${prop}: ${person[prop]}`);
}

// Output:
// name: John
// age: 30
// gender: male
```

2. Object.keys() method: This method returns an array of the object's own enumerable properties (keys), which can be looped through using a for...of loop or forEach() method.
Example:
```js
let person = {
  name: "John",
  age: 30,
  gender: "male"
};

let keys = Object.keys(person);

for (let key of keys) {
  console.log(`${key}: ${person[key]}`);
}

// Output:
// name: John
// age: 30
// gender: male
```

3. Object.values() method: This method returns an array of the object's own enumerable property values, which can be looped through using a for...of loop or forEach() method.
Example:

```js
let person = {
  name: "John",
  age: 30,
  gender: "male"
};

let values = Object.values(person);

for (let value of values) {
  console.log(value);
}

// Output:
// John
// 30
// male
```

4. Object.entries() method: This method returns an array of the object's own enumerable property key-value pairs as arrays, which can be looped through using a for...of loop or forEach() method.
Example:

```js
let person = {
  name: "John",
  age: 30,
  gender: "male"
};

let entries = Object.entries(person);

for (let [key, value] of entries) {
  console.log(`${key}: ${value}`);
}

// Output:
// name: John
// age: 30
// gender: male
```

---
