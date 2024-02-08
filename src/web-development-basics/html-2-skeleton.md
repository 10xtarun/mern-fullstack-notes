# Skeleton or Structure of an HTML Webpage

* DOCTYPE Declaration:
The `<!DOCTYPE html>` declaration is used to specify the version of HTML being used. It should be placed at the very beginning of the HTML document to ensure that the browser renders the page in standards mode.

```html
<!DOCTYPE html>
```

* HTML Root Element:
The `<html>` element serves as the root element of the HTML document and contains all other elements.

```html
<html lang="en">
```
    
> The lang attribute specifies the language of the document, which can help screen readers and search engines understand the content better. Replace "en" with the appropriate language code if necessary.

* Head Section:
The `<head>` section contains meta-information about the document, such as the document title, character encoding, viewport settings, and links to external resources like stylesheets and scripts.

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My HTML Website</title>
    <!-- Additional meta tags, stylesheets, and scripts can be added here -->
</head>
```

> The `<meta charset="UTF-8">` tag specifies the character encoding of the document as UTF-8, which supports a wide range of characters from different languages.

> The `<meta name="viewport" content="width=device-width, initial-scale=1.0">` tag sets the viewport width to the width of the device and sets the initial zoom level to 1.0.


* Body Section:
The `<body>` section contains the main content of the HTML document, including text, images, links, forms, and other elements.

```html
<body>
    <!-- Header Section -->
    <header>
        <!-- Navigation Menu, Logo, etc. -->
    </header>

    <!-- Main Content Section -->
    <main>
        <!-- Content Goes Here -->
    </main>

    <!-- Footer Section -->
    <footer>
        <!-- Footer Content -->
    </footer>
</body>
```
> Header Section (`<header>`): Contains elements such as the navigation menu, logo, and other header-related content.

> Main Content Section (`<main>`): Contains the primary content of the webpage, such as articles, sections, and other relevant content.

> Footer Section (`<footer>`): Contains elements such as copyright information, contact details, and other footer-related content.

* Closing HTML Tag:
Finally, close the HTML document with the `</html>` tag.

```html
</html>
```

> By following this step-by-step structure, you can create a well-organized HTML skeleton for your website. Remember to fill in the content within each section according to your website's requirements.
