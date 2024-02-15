# Arrays in JS

> An array is a collection of elements of any data type that are stored in contiguous memory locations. Arrays are commonly used to store and organize related data.

Arrays in JavaScript are stored as objects in memory, with each element being a property of the array object. The index of each element is used as the property name.

---

## Example of creating an array in JavaScript:

```js
let myArray = [1, 2, 3, 4, 5];
```

In the example above, we have created an array called myArray that contains five elements of type number.

To access elements of an array in JavaScript, we use square brackets with the index of the element we want to access. The first element of an array has an index of 0, the second element has an index of 1, and so on.

* Example of accessing elements of an array in JavaScript:

```js
let myArray = [1, 2, 3, 4, 5];

console.log(myArray[0]); // Output: 1In the example above, we are accessing the first and third elements of the myArray array using their index.
```

* We can also change the value of an array element by assigning a new value to it using its index:
console.log(myArray[2]); // Output: 3

```js
let myArray = [1, 2, 3, 4, 5];

myArray[0] = 6;

console.log(myArray); // Output: [6, 2, 3, 4, 5]
```

In the example above, we are changing the value of the first element of the myArray array from 1 to 6.

* We can also add elements to an array using the push() method, remove elements using the pop() method, or insert elements using the splice() method.

Examples of using these methods:

```js
let myArray = [1, 2, 3, 4, 5];

myArray.push(6);
console.log(myArray); // Output: [1, 2, 3, 4, 5, 6]

myArray.pop();
console.log(myArray); // Output: [1, 2, 3, 4, 5]

myArray.splice(2, 0, 7);
console.log(myArray); // Output: [1, 2, 7, 3, 4, 5]
```

In the examples above, we are adding an element to the end of the myArray array using push(), removing the last element of the array using pop(), and inserting an element at index 2 using splice().

---
