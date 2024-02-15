# Exercise: DOM

What is the Document Object Model (DOM) in JavaScript and how does it work?

Example: Suppose you have an HTML document with a button element that has an id attribute of "myButton". To access this element in JavaScript, you would use the following code:
```js
const button = document.getElementById("myButton");
```

The DOM is a programming interface for web documents that allows JavaScript to interact with HTML and CSS. When a web page is loaded, the browser creates a DOM tree representing the structure of the document, and each element in the tree becomes a node in the DOM. JavaScript can then manipulate these nodes to change the content, style, and behavior of the web page.

--- 

How can you add and remove HTML elements using the DOM in JavaScript?

Example: Suppose you want to add a new paragraph element to the body of an HTML document. You can use the following code:
```js
const newParagraph = document.createElement("p");
const textNode = document.createTextNode("This is a new paragraph.");
newParagraph.appendChild(textNode);
document.body.appendChild(newParagraph);
```

To remove an element from the DOM, you can use the removeChild() method. For example, to remove the first child element of the body element, you can use the following code:
```js
const body = document.body;
const firstChild = body.firstChild;
body.removeChild(firstChild);
```

---

How can you respond to events using the DOM in JavaScript?

Example: Suppose you want to change the text of a paragraph element when a button is clicked. You can use the following code:
```html
<button id="myButton">Click me!</button>
<p id="myParagraph">This is some text.</p>
```
```js
const button = document.getElementById("myButton");
const paragraph = document.getElementById("myParagraph");

button.addEventListener("click", function() {
  paragraph.textContent = "The text has changed!";
});
```

In this example, the addEventListener() method is used to attach a "click" event listener to the button element. When the button is clicked, the anonymous function passed as the second argument is called, which changes the text content of the paragraph element.

---
