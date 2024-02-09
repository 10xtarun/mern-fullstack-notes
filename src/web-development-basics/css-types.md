# Types of CSS:

1. Inline CSS: Inline CSS is applied directly within the HTML elements using the style attribute. This method is useful for applying specific styles to individual elements, but it can make the HTML code less readable and harder to maintain.

Example:
```html
<p style="color: red;">This is a paragraph with inline CSS.</p>
```

2. Internal CSS: Internal CSS is defined within the `<style>` element in the `<head>` section of an HTML document. It applies styles to multiple elements within the same HTML file. While it keeps the styles separate from the HTML content, it still affects only the specific HTML document it is defined in.

Example:
```html
<head>
    <style>
        p {
            color: blue;
        }
    </style>
</head>
<body>
    <p>This is a paragraph with internal CSS.</p>
</body>
```

3. External CSS: External CSS is defined in a separate CSS file with a .css extension. This method allows for the separation of content and presentation, making it easier to maintain and update styles across multiple HTML files. The CSS file is linked to the HTML file using the `<link>` element in the `<head>` section.

Example (styles.css):
```css
p {
    color: green;
}
```

```html
<head>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <p>This is a paragraph with external CSS.</p>
</body>
```

---
