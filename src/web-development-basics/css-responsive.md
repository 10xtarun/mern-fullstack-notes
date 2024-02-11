
# Responsive Web Design

Responsive web design is an approach to designing and developing websites that adapt to different screen sizes and devices. The main goal is to ensure that a website looks and functions well on all devices, from desktop computers to smartphones.

To write responsive CSS, there are several techniques available, including media queries, flexible grid systems, and fluid layouts.

### Media Queries

> different style for different media types

### Media Queries deals with following:
* width and height of the viewport
* width and height of the device
* orientation
* resolution

### What is viewport ?
> The viewport is the area of a web page that's visible to the user.
> The viewport is a rectangle, the size of which is determined by the size of the user's device.

### MQ Syntax
```
@media not|only mediatype and (expressions) {
  CSS-Code;
}
```

> Media queries are a key feature of responsive CSS. They allow you to target specific screen sizes or device types and apply different styles accordingly. For example, you can use a media query to apply different font sizes or adjust the layout of elements on a mobile device.

An example of how to use media queries in CSS to adjust the font size on different devices:
```css
/* Default font size */
body {
  font-size: 16px;
}

/* Media query for smaller screens */
@media only screen and (max-width: 768px) {
  body {
    font-size: 14px;
  }
}

/* Media query for even smaller screens */
@media only screen and (max-width: 480px) {
  body {
    font-size: 12px;
  }
}
```
> Another way to write responsive CSS is to use a flexible grid system, such as Bootstrap or CSS Grid. These systems allow you to create a grid of columns that automatically adjust to different screen sizes. Here is an example using CSS Grid:

```html
<div class="container">
  <div class="row">
    <div class="col">Column 1</div>
    <div class="col">Column 2</div>
    <div class="col">Column 3</div>
  </div>
</div>
```
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
}

@media only screen and (max-width: 768px) {
  .container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media only screen and (max-width: 480px) {
  .container {
    grid-template-columns: 1fr;
  }
}
```
In this example, we create a container with a grid layout and three columns. We use the repeat function to create three columns that each take up one fraction of the available space (1fr). We also add a 20-pixel gap between the columns using the grid-gap property.

We then use media queries to adjust the number of columns as the screen size decreases. For example, on screens smaller than 768 pixels, we switch to a two-column layout, and on screens smaller than 480 pixels, we switch to a single column layout.

Overall, there are many ways to write responsive CSS, and the best approach will depend on the specific needs of your website. However, using media queries and flexible grid systems are two common and effective techniques for creating responsive designs.

---
### Project: Simple responsive gallery
```html
<html>

<head>
    <title> Responsive Image Gallery</title>
    <style>
        body {
            margin: 0;
            padding: 0;
        }

        header {
            text-align: center;
            padding: 1rem auto;
        }

        .row {
            display: flex;
            flex-wrap: wrap;
        }

        .col {
            flex: 25%;
        }

        img {
            width: 100%;
            margin-top: 10px;
        }

        @media screen and (max-width: 800px) {
            .col {
                flex: 50%;
            }
        }

        @media screen and (max-width: 600px) {
            .col {
                flex: 100%;
            }
        }

        
    </style>
</head>

<body>
    <header>
        <h1>A Responsive Image Gallery</h1>
    </header>

    <div class="row">
        <div class="col">
            <img
                src="https://images.unsplash.com/photo-1676238540582-5958404206c2?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8" />

            <img
                src="https://images.unsplash.com/photo-1676365743910-35ba5be051b8?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDE1fHhIeFlUTUhMZ09jfHxlbnwwfHx8fA%3D%3D" />

            <img
                src="https://images.unsplash.com/photo-1676271608840-9712fe255ae0?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDE5fHhIeFlUTUhMZ09jfHxlbnwwfHx8fA%3D%3D" />

            <img
                src="https://images.unsplash.com/photo-1671483330944-36bbbe090e8a?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8" />
        </div>

        <div class="col">
            <img
                src="https://images.unsplash.com/photo-1580664090511-35bbc93df9c1?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDcxfHhIeFlUTUhMZ09jfHxlbnwwfHx8fA%3D%3D" />


            <img
                src="https://images.unsplash.com/photo-1676365743910-35ba5be051b8?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDE1fHhIeFlUTUhMZ09jfHxlbnwwfHx8fA%3D%3D" />


            <img
                src="https://images.unsplash.com/photo-1671483330944-36bbbe090e8a?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8" />

            <img
                src="https://images.unsplash.com/photo-1676238540582-5958404206c2?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8" />

        </div>

        <div class="col">
            <img
                src="https://images.unsplash.com/photo-1676271608840-9712fe255ae0?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDE5fHhIeFlUTUhMZ09jfHxlbnwwfHx8fA%3D%3D" />

            <img
                src="https://images.unsplash.com/photo-1671483330885-62abe0be18a6?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDYyfHhIeFlUTUhMZ09jfHxlbnwwfHx8fA%3D%3D" />

            <img
                src="https://images.unsplash.com/photo-1671483330944-36bbbe090e8a?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8" />

            <img
                src="https://images.unsplash.com/photo-1676238540582-5958404206c2?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8" />


        </div>

        <div class="col">
            <img
                src="https://images.unsplash.com/photo-1676238540582-5958404206c2?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8" />

            <img
                src="https://images.unsplash.com/photo-1671727337787-a08619e22c78?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDY0fHhIeFlUTUhMZ09jfHxlbnwwfHx8fA%3D%3D" />

            <img
                src="https://images.unsplash.com/photo-1676271608840-9712fe255ae0?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDE5fHhIeFlUTUhMZ09jfHxlbnwwfHx8fA%3D%3D" />

            <img
                src="https://images.unsplash.com/photo-1671483330944-36bbbe090e8a?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8" />

        </div>
    </div>
</body>

</html>
```

---