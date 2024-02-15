# JS Fundamentals

## Data types in JavaScript

### Primitive data types

1. String: used to represent textual data, such as names or messages. Strings are enclosed in single or double quotes.

2. Number: used to represent numerical data, including integers and floating-point numbers.

3. Boolean: used to represent true/false values.

4. Undefined: used to represent the absence of a value. A variable that has not been assigned a value is undefined.

5. Null: used to represent the intentional absence of any object value.

6. Symbol: a new data type added in ES6, which represents a unique identifier. Symbols are often used as keys in objects.

### JavaScript also has one non-primitive data type

7. Object: used to represent complex data structures, such as arrays, functions, and objects. Objects are a key feature of JavaScript, and many of the language's features are built around them.

---

## Example of how variables are declared, initialized and accessed in JavaScript:

```js
// Declare a variable called 'name'
let name;

// Initialize the variable 'name' with the value 'John'
name = 'John';

// Declare and initialize a variable called 'age' with the value 30
let age = 30;

// Print the values of 'name' and 'age' to the console
console.log(name);
console.log(age);
```

Let's break down each line and see what it does:

1. let name; declares a variable called 'name' without initializing it. This is known as a variable declaration.

2. name = 'John'; assigns the value 'John' to the variable 'name'. This is known as variable initialization.

3. let age = 30; declares and initializes a variable called 'age' with the value 30.

4. console.log(name); prints the value of 'name' to the console. The console is a tool used in web development that displays messages and logs in real-time, and is accessible through the developer console of most modern web browsers.

5. console.log(age); prints the value of 'age' to the console.

When you run this code in a JavaScript environment, such as a web browser console or a NodeJS environment, you will see the values of 'name' and 'age' printed to the console:

```js
John
30
```

In this example, we used the let keyword to declare variables, which is the recommended way to declare variables in modern JavaScript. The let keyword allows us to declare variables that can be reassigned to a new value later on in the program. 

---


## Variable Declaration and Initialization in JS

In JavaScript, variables are stored in memory as part of the execution context. When a variable is declared, space is reserved in memory to store its value.

When a variable is accessed in JavaScript, the engine looks up the variable in memory and retrieves its value. This process is known as variable resolution.

Here's what happens behind the scenes of JavaScript when a variable is declared and defined:

1. Declaration: When a variable is declared using the let, const, or var keyword, the JavaScript engine creates a new identifier in memory with the name of the variable. The identifier is assigned a reference to a memory location where the value of the variable will be stored.

2. Initialization: When a variable is initialized, the engine assigns a value to the memory location that was reserved for the variable. If the variable is not initialized at the time of declaration, its value is set to undefined.

3. Assignment: When a value is assigned to a variable using the = operator, the value is stored in the memory location reserved for the variable.

4. Scope: Variables in JavaScript are scoped to the function or block in which they are declared. This means that variables declared inside a function are not accessible outside of the function.

5. Garbage Collection: When a variable is no longer needed, JavaScript automatically removes it from memory through a process called garbage collection. This frees up memory that can be used by other parts of the program.

> It's important to note that variables in JavaScript are dynamically typed, which means that their data type can change during the execution of the program. This is in contrast to statically typed languages, where the data type of a variable is fixed at compile time.

---

## Data type: String

> In JavaScript, a string is a sequence of characters enclosed in single or double quotes. Strings are one of the most common data types in JavaScript and are used to represent text.

### Common string manipulation in JS are:

* Concatenation: You can concatenate two or more strings using the + operator. For example, if you have two strings "hello" and "world", you can concatenate them like this:

```js
let greeting = "hello";
let name = "world";
let message = greeting + " " + name;
console.log(message); // Output: "hello world"
```

* String Length: You can find the length of a string using the length property. For example:

```js
let myString = "This is a string";
console.log(myString.length); // Output: 16
```

* Accessing Characters: You can access individual characters in a string using square brackets and the index of the character you want. For example:
javascript

```js
let myString = "hello";
console.log(myString[0]); // Output: "h"
console.log(myString[3]); // Output: "l"
```

* Substring: You can extract a portion of a string using the substring method. For example:

```js
let myString = "hello world";
let subString = myString.substring(0, 5); // Extracts the first 5 characters
console.log(subString); // Output: "hello"
```

* Replace: You can replace one or more occurrences of a substring in a string using the replace method. For example:

```js
let myString = "hello world";
let newString = myString.replace("world", "javascript");
console.log(newString); // Output: "hello javascript"
```

### Important features of string in JS are:

1. Strings are immutable: This means that once you create a string, you cannot change the individual characters in it. Instead, you must create a new string with the desired changes.

2. Strings are iterable: This means that you can loop over the characters in a string using a for loop or other iterable methods like forEach or map.

3. Strings have many built-in methods: JavaScript provides many methods for working with strings, such as substring, replace, and split. These methods make it easy to manipulate strings in various ways.

4. Strings can be converted to other data types: You can convert a string to a number using the parseInt or parseFloat methods. You can also convert a string to an array using the split method.

> Overall, strings are an essential data type in JavaScript and are used extensively in web development. Understanding how to manipulate strings is crucial for building effective JavaScript applications.

---

## Data type: Undefined and Null

In JavaScript, both undefined and null are special values that represent the absence of a value or an empty value. However, they are not interchangeable, and they have slightly different meanings.

### Undefined
undefined is a primitive value that represents a variable that has been declared but has not been assigned a value. It also represents a function that has been defined but has no return statement.

Here's an example of a variable that is declared but not assigned a value:

```js
let foo;
console.log(foo); // Output: undefined
```

In this example, the variable foo is declared but not assigned a value. When we try to log the value of foo to the console, we get undefined.

Here's an example of a function that does not have a return statement:

```js
function bar() {}
console.log(bar()); // Output: undefined
```

In this example, the function bar is defined but does not have a return statement. When we call the function and try to log the return value to the console, we get undefined.

### Null
null is also a primitive value that represents the intentional absence of any object value. It is often used to indicate that a variable or object property has no value.

Here's an example of a variable that is explicitly set to null:

```js
let bar = null;
console.log(bar); // Output: null
```

In this example, the variable bar is explicitly set to null. When we log the value of bar to the console, we get null.

Here's an example of an object property that is set to null:

```js
const person = {
  name: 'John',
  age: null,
};
console.log(person.age); // Output: null
```

In this example, the age property of the person object is set to null. When we log the value of person.age to the console, we get null.

### Difference between Undefined and Null 
The main difference between undefined and null is that undefined is the default value of a variable that has not been assigned a value, whereas null is an intentional absence of any object value. undefined is also a primitive value, whereas null is an object value. In general, you should use undefined to represent the absence of a value that should have been assigned, and use null to represent the intentional absence of any object value (empty).

---

## Data type: Number

The Number data type in JavaScript is used to represent numeric values, both integers and floating-point numbers.

Some examples of numbers declaration in JavaScript:

```js
let integer = 42; // integer number
let floatingPoint = 3.14; // floating-point number
let negativeNumber = -10; // negative number
let scientificNotation = 2.998e8; // scientific notation
```

The core features of the Number data type in JavaScript include the ability to perform arithmetic operations such as addition, subtraction, multiplication, and division. It also supports several mathematical methods such as Math.sqrt() (to find the square root), Math.pow() (to raise a number to a power), and Math.abs() (to find the absolute value of a number).

Examples of number-related manipulations in JavaScript:

```js
let x = 10;
let y = 5;

// Addition
let sum = x + y; // 15

// Subtraction
let difference = x - y; // 5

// Multiplication
let product = x * y; // 50

// Division
let quotient = x / y; // 2

// Remainder (modulo)
let remainder = x % y; // 0

// Exponentiation
let exponentiation = x ** y; // 100000

// Square root
let squareRoot = Math.sqrt(x); // 3.1622776601683795

// Absolute value
let absoluteValue = Math.abs(-10); // 10
```

Additionally, JavaScript provides several methods for converting strings to numbers and vice versa. For example, the parseInt() method can be used to convert a string to an integer, and the parseFloat() method can be used to convert a string to a floating-point number.

```js
let stringNumber = "42";
let parsedInteger = parseInt(stringNumber); // 42

let stringFloat = "3.14";
let parsedFloat = parseFloat(stringFloat); // 3.14
```

It is worth noting that JavaScript's Number data type has some limitations due to the way it represents numbers internally. Specifically, it can only represent numbers up to a certain precision (approximately 15-17 decimal digits), and certain arithmetic operations can lead to rounding errors. Therefore, it is important to be aware of these limitations when working with large numbers or performing precise calculations.

---

## Data type: Boolean

Boolean data type is used to represent logical values - true or false. It is a primitive data type, meaning that it is not an object and does not have any methods or properties.

Examples of Boolean values in JavaScript:

```js
let isTrue = true;
let isFalse = false;
```

In addition to these literal values, Boolean values can also be the result of logical expressions. For example:

```js
let x = 10;
let y = 5;

let greaterThan = x > y; // true
let lessThan = x < y; // false
let isEqual = x === y; // false
let notEqual = x !== y; // true
```

Here, the expressions x > y, x < y, x === y, and x !== y all evaluate to Boolean values - either true or false - based on the comparison being made.

Boolean values are often used in conditional statements to control the flow of a program. For example:

```js
let age = 18;

if (age >= 18) {
  console.log("You are old enough to vote.");
} else {
  console.log("You are not old enough to vote.");
}
```

---
