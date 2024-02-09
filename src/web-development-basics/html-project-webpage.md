# Create a basic webpage in HTML:

> In this project, we'll create a basic webpage for a fictional restaurant. We'll include elements such as headings, paragraphs, images, links, lists, forms, and more.

Here's a step-by-step guide to creating the HTML project:

1. Create a New HTML File:
Create a new file with a .html extension, such as index.html, using a text editor or an HTML editor like Visual Studio Code, Sublime Text, or Notepad++.

2. HTML Structure:
Start by defining the basic structure of the HTML document using the `<!DOCTYPE html>` declaration and the `<html>, <head>, and <body>` elements.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Restaurant Website</title>
</head>
<body>

</body>
</html>
```

3. Header Section:
Add a header section containing the restaurant's name and a navigation menu.

```html
<header>
    <h1>My Restaurant</h1>
    <nav>
        <ul>
            <li><a href="#home">Home</a></li>
            <li><a href="#menu">Menu</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>
</header>
```

4. Main Content Section:
Add a main content section with information about the restaurant, including an image, a paragraph, and a list of menu items.

```html
<main>
    <section id="home">
        <h2>Welcome to Our Restaurant</h2>
        <img src="restaurant.jpg" alt="Restaurant Image">
        <p>We serve delicious dishes made with fresh ingredients.</p>
    </section>
    <section id="menu">
        <h2>Menu</h2>
        <ul>
            <li>Appetizers</li>
            <li>Main Courses</li>
            <li>Desserts</li>
        </ul>
    </section>
</main>
```

5. Footer Section:
Add a footer section with contact information and social media links.

```html
<footer id="contact">
    <p>Contact Us:</p>
    <p>123 Restaurant Street, City</p>
    <p>Email: info@example.com</p>
    <p>Phone: 123-456-7890</p>
    <nav>
        <ul>
            <li><a href="#">Facebook</a></li>
            <li><a href="#">Twitter</a></li>
            <li><a href="#">Instagram</a></li>
        </ul>
    </nav>
</footer>
```

6. Closing Tags:
Close the remaining tags to ensure proper structure.

```html
</body>
</html>
```

7. Add CSS (Optional):
Optionally, you can add CSS styles to enhance the appearance of your webpage. You can either use inline styles within the HTML document or link an external CSS file.

Example of inline styles:
```html
<header style="background-color: #333; color: #fff; padding: 10px;">
```

> That's it! You've created a basic HTML project for a restaurant website.

---

# Add CSS to above web page:

1. Create a CSS File:
First, create a new file named styles.css in the same directory as your HTML file.

2. Link CSS File to HTML:
In the `<head>` section of your HTML file, add a link to the CSS file using the `<link>` element. This allows the browser to apply the styles defined in the CSS file to the HTML content.

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Restaurant Website</title>
    <link rel="stylesheet" href="styles.css">
</head>
```

3. Define Global Styles:
Start by defining global styles that apply to the entire webpage. In this case, we'll set the font family, margin, padding, and background color for the `<body>` element.

```css
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f5f5f5;
}
```

> These styles ensure a consistent look and feel across the entire webpage by setting the default font family, removing any default margin and padding, and setting a background color.

4. Define Header Styles:
Next, define styles for the header section of the webpage. We'll set the background color, text color, padding, and text alignment for the `<header>` element. We'll also style the heading (`<h1>`) and the navigation links (`<nav> and <ul>`).

```css
header {
    background-color: #333;
    color: #fff;
    padding: 10px;
    text-align: center;
}

header h1 {
    margin: 0;
}

nav ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}

nav ul li {
    display: inline;
    margin-right: 20px;
}

nav ul li a {
    color: #fff;
    text-decoration: none;
}
```

> These styles define the appearance of the header section, including its background color, text color, padding, and text alignment. They also style the heading and navigation links for better readability and visual appeal.

5. Define Main Content Styles:
Define styles for the main content section of the webpage. We'll set padding for the `<main>` element and margin-bottom for `<section>` elements.

```css
main {
    padding: 20px;
}

section {
    margin-bottom: 20px;
}
```

> These styles add spacing and separation between different sections of the main content, improving readability and visual hierarchy.

6. Define Footer Styles:
Finally, define styles for the footer section of the webpage. We'll set the background color, text color, padding, and text alignment for the `<footer>` element. We'll also style the paragraph (`<p>`) and navigation links (`<nav> and <ul>`).

```css
footer {
    background-color: #333;
    color: #fff;
    padding: 20px;
    text-align: center;
}

footer p {
    margin: 5px 0;
}

footer nav ul li {
    display: inline;
    margin-right: 10px;
}

footer nav ul li a {
    color: #fff;
    text-decoration: none;
}
```

> These styles define the appearance of the footer section, including its background color, text color, padding, and text alignment. They also style the paragraphs and navigation links for better visual appeal and accessibility

> That's it! You've successfully added CSS styles to the HTML project for the restaurant website, enhancing its appearance and layout. Each CSS rule serves a specific purpose in defining the visual presentation of different elements on the webpage.

---

