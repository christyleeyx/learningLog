# CSS Notes

This is a slow accumulation of my CSS concepts compiled from various resources.

Main useful resources:

1. [MDN Web Docs / CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)

2. [W3 Schools CSS References](https://www.w3schools.com/cssref/index.php)

###Typography

#### html selector

#### dividers

border-bottom: 2px solid #

#### letter-spacing

#### rem

#### Adding google fonts to your sheet

1. getting the ref link from google fonts
2. linking
3. referencing in selectors

#### Box-sizing

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
