# Exercise: Array

> ## Practice Exercises: JavaScript
> Note: These questions are meant to guide you through different topics and methods to solve. It is expected that you should explore these topics on your own and practice more as much as possible.

---

What will be the output of the following code?
```js
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let arr3 = arr1.concat(arr2);

console.log(arr3);
```

Answer: [1, 2, 3, 4, 5, 6]

Explanation: concat() method concatenates two or more arrays and returns a new array containing the elements from all the arrays. In this case, it will return a new array [1, 2, 3, 4, 5, 6].

---

What will be the output of the following code?
```js
let arr = [1, 2, 3, 4, 5];
let slicedArr = arr.slice(1, 3);

console.log(slicedArr);
```

Answer: [2, 3]

Explanation: slice() method returns a new array containing the elements from the start index to the end index. In this case, it will return a new array [2, 3].

---

What will be the output of the following code?
```js
let arr = [1, 2, 3];
arr.push(4);

console.log(arr);
```

Answer: [1, 2, 3, 4]

Explanation: push() method adds one or more elements to the end of an array and returns the new length of the array. In this case, it will add the element 4 to the end of the array and return a new array [1, 2, 3, 4].

---

What will be the output of the following code?
```js
let arr = [1, 2, 3];
let poppedElement = arr.pop();

console.log(poppedElement);
```

Answer: 3

Explanation: pop() method removes the last element from an array and returns that element. In this case, it will remove the last element 3 from the array and return it.

---

What will be the output of the following code?
```js
let arr = [1, 2, 3];
let reversedArr = arr.reverse();

console.log(reversedArr);
```

Answer: [3, 2, 1]

Explanation: reverse() method reverses the order of the elements in an array and returns the reversed array. In this case, it will return a new array [3, 2, 1].

---

Write a function that takes an array of numbers and returns a new array containing only the even numbers.
```js
function getEvenNumbers(arr) {
  let evenArr = [];
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] % 2 === 0) {
      evenArr.push(arr[i]);
    }
  }
  return evenArr;
}

// Example usage:
let numbers = [1, 2, 3, 4, 5, 6, 7, 8];
let evenNumbers = getEvenNumbers(numbers);
console.log(evenNumbers); // Output: [2, 4, 6, 8]
```

---

Write a function that takes an array of strings and returns a new array containing only the strings that have a length greater than 5.
```js
function getLongStrings(arr) {
  let longStrings = [];
  for (let i = 0; i < arr.length; i++) {
    if (arr[i].length > 5) {
      longStrings.push(arr[i]);
    }
  }
  return longStrings;
}

// Example usage:
let strings = ['apple', 'banana', 'pear', 'pineapple', 'grapefruit'];
let longStrings = getLongStrings(strings);
console.log(longStrings); // Output: ['pineapple', 'grapefruit']
```

---

How can you filter an array of objects based on a certain condition using Array.filter() method in JavaScript?
```js
const persons = [
  { name: 'John', age: 24 },
  { name: 'Jane', age: 30 },
  { name: 'Mary', age: 19 },
  { name: 'Peter', age: 40 }
];

const filteredPersons = persons.filter(person => person.age >= 30);

console.log(filteredPersons); // [{ name: 'Jane', age: 30 }, { name: 'Peter', age: 40 }]
```

In this example, the Array.filter() method is used to filter an array of objects based on a condition. In this case, we want to filter the persons array to include only those objects where the age property is greater than or equal to 30. The Array.filter() method takes a callback function as an argument which returns a boolean value based on the condition. If the callback function returns true, the object is included in the filtered array, otherwise it is excluded.

---

How can you use the Array.map() method in JavaScript to transform an array of objects to another format?
```js
const persons = [
  { name: 'John', age: 24 },
  { name: 'Jane', age: 30 },
  { name: 'Mary', age: 19 },
  { name: 'Peter', age: 40 }
];

const formattedPersons = persons.map(person => {
  return {
    firstName: person.name,
    age: person.age
  };
});

console.log(formattedPersons);
// [{ firstName: 'John', age: 24 }, { firstName: 'Jane', age: 30 }, { firstName: 'Mary', age: 19 }, { firstName: 'Peter', age: 40 }]
```

In this example, the Array.map() method is used to transform an array of objects to another format. In this case, we want to create a new array of objects where the name property is renamed to firstName. The Array.map() method takes a callback function as an argument which returns the transformed object. The returned value is used to create a new array.

---

How can you use the Array.reduce() method in JavaScript to calculate the sum of an array of numbers?
```js
const numbers = [5, 10, 15, 20];

const sum = numbers.reduce((accumulator, currentValue) => {
  return accumulator + currentValue;
}, 0);

console.log(sum); // 50
```

In this example, the Array.reduce() method is used to calculate the sum of an array of numbers. The Array.reduce() method takes a callback function as an argument which takes two arguments: the accumulator and the currentValue. The accumulator is the accumulated value of the previous iterations, and the currentValue is the current element being processed. The callback function returns the accumulated value which is passed on to the next iteration. In this case, we start with an initial value of 0, and in each iteration, we add the currentValue to the accumulator.

---
