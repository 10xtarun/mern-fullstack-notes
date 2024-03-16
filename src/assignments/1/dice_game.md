# Dice Game UI

## Overview

In this project, we will create a simple user interface (UI) for a dice game using HTML and CSS. The UI will consist of dice images and a button to roll the dice. The goal is to provide a visually appealing interface for users to interact with while playing the dice game.

> Modify the project as per your mentor's instructions.

## Project Structure:]

* HTML File (index.html): Contains the structure of the webpage.
* CSS File (styles.css): Contains the styles to customize the appearance of the webpage.
* Dice Images: Images of dice faces (e.g., dice1.png, dice2.png, etc.) to display on the UI.

## Steps to Create the Dice Game UI:

### Step 1: Set Up HTML Structure

Create an HTML file named index.html.
Define the basic structure of the webpage using HTML tags such as `<html>, <head>, <body>, and <div>`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dice Game</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Dice Game</h1>
        <div class="dice"></div>
        <button class="roll-btn">Roll Dice</button>
    </div>
</body>
</html>
```

### Step 2: Style the UI Using CSS

Create a CSS file named styles.css.
Style the container, dice, and button elements to enhance the appearance of the UI.

```css
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    text-align: center;
}

.dice {
    width: 150px;
    height: 150px;
    background-image: url('dice.png'); /* Replace 'dice.png' with the path to your dice image */
    background-size: cover;
    margin: 20px auto;
}

.roll-btn {
    padding: 10px 20px;
    font-size: 18px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.roll-btn:hover {
    background-color: #0056b3;
}
```

### Step 3: Add Dice Images

Download or create images of dice faces (e.g., dice1.png, dice2.png, etc.).
Place the dice images in the same directory as your HTML file.

### Step 4: Final Touches

Open the index.html file in a web browser to view the Dice Game UI.
Click the "Roll Dice" button to roll the dice and see the result.

> This simple Dice Game UI will provide users with a visually appealing interface to roll the dice and enjoy the game.

---
