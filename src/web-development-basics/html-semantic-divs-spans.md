# What is semantic HTML?

Semantic HTML refers to the practice of using HTML elements to convey the meaning and structure of the content they contain. Semantic HTML aims to make the structure of a web page more meaningful and understandable to both browsers and developers. By using semantic HTML, developers can improve accessibility, search engine optimization (SEO), and maintainability of their web pages.

Semantic HTML elements are those that have a specific meaning and purpose, and they describe their content in a meaningful way. Examples of semantic HTML elements include `<header>, <nav>, <main>, <section>, <article>, <aside>, <footer>, <h1> to <h6>, <p>, <ul>, <ol>, <li>, <blockquote>, <cite>, <figure>, <figcaption>`, etc.

Example of Semantic HTML:
```html
<header>
    <h1>Website Title</h1>
    <nav>
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">About</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>
</header>
<main>
    <section>
        <h2>About Us</h2>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
    </section>
    <section>
        <h2>Services</h2>
        <ul>
            <li>Service 1</li>
            <li>Service 2</li>
            <li>Service 3</li>
        </ul>
    </section>
</main>
<footer>
    <p>&copy; 2023 Company Name</p>
</footer>
```

# What is non-semantic HTML?

Non-semantic HTML, on the other hand, refers to the use of generic or presentational HTML elements that do not convey any specific meaning or structure to the content they contain. Non-semantic HTML elements are often used purely for styling purposes and do not provide any meaningful information about the content.

Example of Non-semantic HTML:
```html
<div class="header">
    <h1>Website Title</h1>
    <ul class="navigation">
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Contact</a></li>
    </ul>
</div>
<div class="main-content">
    <div class="about">
        <h2>About Us</h2>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
    </div>
    <div class="services">
        <h2>Services</h2>
        <ul>
            <li>Service 1</li>
            <li>Service 2</li>
            <li>Service 3</li>
        </ul>
    </div>
</div>
<div class="footer">
    <p>&copy; 2023 Company Name</p>
</div>
```

In the non-semantic example above, `<div>` elements are used with class attributes to create layout structures, but they do not provide any information about the purpose or meaning of the content they contain. This makes it harder for both browsers and developers to understand the structure and meaning of the content.

> Overall, using semantic HTML helps improve the accessibility, SEO, and maintainability of web pages by providing clear and meaningful structure to the content.

---

# Elements classifications in HTML:

> In HTML, elements are classified into two main categories: block-level elements and inline elements.

### Block-Level Elements:

Block-level elements are elements that create a block of content and typically start on a new line, extending the full width available to them. They stack on top of each other vertically. Block-level elements are used to structure the layout of a webpage and typically contain other block-level or inline elements.

Examples of block-level elements include `<div>, <p>, <h1> to <h6>, <ul>, <ol>, <li>, <header>, <footer>, <section>, <article>`, etc.

Example:
```html
<div>This is a block-level element.</div>
<p>This is another block-level element.</p>
```

### Inline Elements:

Inline elements are elements that do not start on a new line and only take up as much width as necessary. They flow within the content and allow other elements to sit beside them horizontally. Inline elements are typically used for styling or marking up small pieces of text within a block of content.

Examples of inline elements include `<span>, <a>, <strong>, <em>, <img>, <input>, <button>, <br>, <a>`, etc.

Example:
```html
<span>This is an inline element.</span>
<a href="#">This is another inline element (link).</a>
```

### Divs and Spans:

`<div>` and `<span>` are generic container elements used for grouping and styling content in HTML.

`<div>` (division) is a block-level element that is used to group together other block-level or inline elements. It is commonly used for creating layout structures and styling sections of a webpage.

Example:
```html
<div>
    <h1>This is a heading inside a div.</h1>
    <p>This is a paragraph inside a div.</p>
</div>
```

`<span>` is an inline element that is used to apply styles or markup to a specific piece of text within a block of content. It is commonly used for applying styles using CSS or for marking up small pieces of text.

Example:
```html
<p>This is a <span style="color: blue;">blue</span> text.</p>
```

> In summary, block-level elements create blocks of content that start on a new line and take up the full width available, while inline elements flow within the content and only take up as much width as necessary. `<div>` and `<span>` are generic container elements used for grouping and styling content, with `<div>` being block-level and `<span>` being inline.

---
