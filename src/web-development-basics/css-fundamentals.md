# CSS Fundamentals

1. Selectors:
Selectors are patterns used to select HTML elements that you want to style. They target specific elements based on their tag name, class, ID, attributes, or relationships with other elements. CSS selectors allow you to apply styles to specific elements or groups of elements.

Example:

```css
/* Tag selector */
p {
    color: blue;
}

/* Class selector */
.highlight {
    background-color: yellow;
}

/* ID selector */
#header {
    font-size: 24px;
}
```

2. Properties:
Properties are the characteristics or attributes of HTML elements that you can style using CSS. Properties define how elements look, such as their color, size, font, margin, padding, and more. Each property has a name and a value, which specify the desired style.

Example:

```css
/* Property: Value */
color: blue;
font-size: 16px;
margin-top: 20px;
```

3. Values:
Values are the specific settings applied to CSS properties. Values can be keywords, numeric values, colors, lengths, percentages, or other valid CSS data types. Different properties accept different types of values, and the values you choose determine the appearance of the styled elements.

Example:

```css
/* Keyword value */
font-family: Arial, sans-serif;

/* Numeric value */
font-size: 18px;

/* Color value */
color: #ff0000;

/* Length value */
margin-top: 10px;

/* Percentage value */
width: 50%;
```

4. Selectors and Declarations:
CSS rules consist of selectors and declarations. Selectors target HTML elements, and declarations define the styles to be applied to those elements. Declarations consist of properties and their corresponding values.

Example:

```css
/* Selector */
p {
    /* Declaration */
    color: blue;
    font-size: 16px;
}
```

5. Cascading:
Cascading refers to the process of combining multiple CSS rules to determine the final styles applied to an element. CSS rules can be defined in different stylesheets, inline styles, or in the same stylesheet with different levels of specificity. The browser applies the styles based on the specificity of the selectors and the order of precedence.

Example:

```css
<style>
    p {
        color: blue; /* Applied */
    }
    p {
        color: red; /* Overridden by the previous rule */
    }
</style>
```

6. Inheritance:
Inheritance is the process by which certain CSS properties are passed from parent elements to their children. When a property is applied to a parent element, its value can be inherited by its child elements unless overridden by a more specific rule. Not all properties are inherited, and the inheritance behavior varies depending on the property.

Example:

```css
/* Applied to the parent element */
.parent {
    font-family: Arial, sans-serif;
}

/* Inherited by the child element */
.child {
    /* Inherits font-family: Arial, sans-serif */
}
```

---

