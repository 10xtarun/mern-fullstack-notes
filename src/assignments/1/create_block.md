# Create a counter block

## Project Idea

Create a block having :

* ⁠Input field
* 4 buttons (+1 , -1 , +10, -10)
* (Value of the number should be Incremented the number of times the value present on the button when a button is pressed )
    <!-- * [UI example attached above. Changes can be made to your liking ] -->

Here's a sample HTML and CSS block with an input field and four buttons:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Number Incrementer</title>
    <style>
        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 50px;
        }

        input {
            width: 200px;
            padding: 10px;
            margin-bottom: 20px;
            font-size: 16px;
            text-align: center;
        }

        button {
            width: 100px;
            padding: 10px;
            margin: 5px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <input type="number" id="numberInput" value="0" readonly>
        <button onclick="increment(1)">+1</button>
        <button onclick="increment(-1)">-1</button>
        <button onclick="increment(10)">+10</button>
        <button onclick="increment(-10)">-10</button>
    </div>

    <script>
        function increment(value) {
            const numberInput = document.getElementById('numberInput');
            let currentValue = parseInt(numberInput.value);
            currentValue += value;
            numberInput.value = currentValue;
        }
    </script>
</body>
</html>
```

This HTML code creates a block with an input field and four buttons. The buttons allow you to increment the value in the input field by either 1, -1, 10, or -10 each time they are clicked. The value in the input field is updated accordingly using JavaScript.

---
