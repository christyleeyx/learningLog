# CSS Notes

This is a slow accumulation of my CSS concepts compiled from various resources.

Main useful resources:

1. [MDN Web Docs / CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)

2. [W3 Schools CSS References](https://www.w3schools.com/cssref/index.php)

## Selectors

```css
selector {
    property: value;
}
```
### CSS Cascades
*Order in which styles are declared matters!!*
styles are applied from top to bottom, overwriting any repeated selectors.

### Specifcity
Specificity is how the browser decides which rules to apply when multiple rules could apply to the same element. 

It is a measure of how specific a given selector is. The more specific selector "wins"

A specificity calculator is used.
> Inline Styles > ID > Class, Attribute, & Pseudo-class Selectors > Element, Pseudo Element selectors

e.g. element vs element descendant

### Inheritance

Sometimes there are no declarations defining the value of a property. The CSS cascade module defines how these missing values should be set via inheritance or from the property's initial value.

----------

- `*universal selectors* (*)`
- `*element selector* (buttons, h1, h2, p)`
- `*id selector* (#id)` - can only be applied to one element
- `*class selector* (.class)` - can be used repeatedly
- `*descendant selector* (e.g. li a)` `- selecting descendents
- `*adjacent selector* (e.g. h1 + button)` - selects only the buttons that are immediately after a h1 
- `*direct child selector* (e.g. div > li)` - selects ony the `<li>`s that are direct children of a `<div>` element
- `*attribute selector* (h1[type/class/id="text"])` - selects all h1 elements where the type or class or id attribute is set to "text"

### Pseudo Classes
keywords added to a selector that specifies a special state of the selected element(S)

#### `:hover`
matches when user hovers with their mouse over an element 

e.g. 
```css
/* When button is hovered over, it's background turns red, text turns white */
.post button:hover {
    background-color: red;
    coloe: white;
    font-weight: 800;
}
```
#### `:active`
matches an element that is activated by the user (usually when clicked)

```css
button:active {
    background-color: red;
    text-decoration: underline;
}
```

#### `:checked`
represents any radio, checkbox, or option element that is checked or toggled to an **on** state

#### `:nth-of-type`
represents elements of a given type, based on their position among a group of siblings

e.g. Website contains a list of posts, you want to use a darker color on every other one

```css
.post: nth-of-type(2n){
    background-color: dark green;
}
```
### Pseudo Elements
Keywords added to a selector that lets you style a particular part of selected element(s)

#### `::first-letter`
applies styles to the first letter of the first line of a block container, but only when not preceded by other content (such as images or inline tables)

```css
p::first-letter {
  font-size: 1.5rem;
  font-weight: bold;
  color: brown;
}

```
#### `::selection`
applies styles to part of a document that has been highlighted/selected by the user

```
p::selection {
  color: red;
  background-color: yellow;
}
```



## Typography

### html selector

### dividers

border-bottom: 2px solid #

### letter-spacing

### rem

### Adding google fonts to your sheet

1. getting the ref link from google fonts
2. linking
3. referencing in selectors

### Box-sizing

_Defines how the width and height of an element are calculated: should they include padding or borders?_

Border-box vs Content-box
![Border-box vs Content-box](/freecodecamp/css/1.%20css%20docs/images/box-sizing.PNG)

`content-box`(default):

- `width` and `height` assigned to element only applies to the content box, which excludes any `border` or `padding`
- e.g. if element's `width` is set to 300px and hence content box only, a border of 5px, padding of 5px will add 20px total. The total width will be 320px.

`border-box`:

- instructs browser to account for `border` and `padding` values in the `width`
- e.g. if an element's `width` is set to 300px. The 20px total of `border` and `padding` are inclusive. This also means that the content box will shrink to absorb that extra width

> Generally `border-box` is easier to deal with while not dealing with the accuracy of your pixels. But when using `position: relative/absolute`, `content-box` allows the positioning values to be relative to the content, and independent of changes to border and padding sizes which is sometimes desirable

## Accessibility 
