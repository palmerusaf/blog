# How to style a `<select/>` tag the easy way.

<!--toc:start-->

- [Problem](#problem)
- [The Hard Way](#the-hard-way)
  - [Build your own](#build-your-own)
  - [Import from a Library](#import-from-a-library)
- [The Easy Way](#the-easy-way)
  - [The Mask](#the-mask)
  - [Code](#code)
  - [Result](#result)
- [Conclusion](#conclusion)

<!--toc:end-->

## Problem

Form controls are notoriously difficult to style, this is especially true with the `<select/>` tag. Between the browsers Firefox respects your style choices the most, followed by Chrome, then Web-kit. The results can be seen below.

![problem demo](https://github.com/palmerusaf/blog/blob/main/01-Style-Select-Tag/problem-demo.png?raw=true)

As you can see above Web-kit in particular is a mess.

And if you want to style/remove elements inside the select box you can forget about it. WYSIWYG.

## The Hard Way

We have a couple of options here.

1. Build a custom select component from scratch.
2. Import a custom select component from a library.

### Build your own

If you need absolute control over all parts of your select component, then building from scratch is the way to go. This CSS-Tricks [article](https://css-tricks.com/striking-a-balance-between-native-and-custom-select-elements/) is an excellent resource if you want to go that route.

The drawback to this approach is that building your own is not trivial, especially if you plan on making it responsive.

### Import from a Library

If you go this route you can save lots of time. If it's a popular library you benefit from experienced UI designers and A/B testing. One popular option is [Material UI](https://mui.com/material-ui/react-select/).

One of the drawbacks is that you're at the mercy of the maintainer. You will also have to take the time to learn the library's API. The component might not fit exactly with your existing styling and it can be difficult to customize. You also could be shipping lots of unnecessary code.

## The Easy Way

What if all you want to do is style your select button and you don't care if the select options are styled?

Just make a mask.

### The Mask

![mask meme](https://github.com/palmerusaf/blog/blob/main/01-Style-Select-Tag/mask-meme.jpg?raw=true)

A mask, also known as a wrapper, is a stylable non-semantic element that goes over your select tag. The idea is you style the div however you want and then you sneak your select tag inside it like a ninja.

### Code

This is what the HTML would look like.

```html
<div class="select-container">
  <span class="angle-bracket rotate-left"> &lt; </span>
  <span>Select</span>
  <span class="angle-bracket rotate-right"> &gt; </span>
  <select class="hidden-select">
    <option selected value="">Select</option>
    <option value="1">Value 1</option>
    <option value="2">Value 2</option>
    <option value="3">Value 3</option>
  </select>
</div>
```

And this is what the CSS would look like.

```css
.select-container {
  display: flex;
  position: relative;
  gap: 2px;
  padding: 2px 4px;
  background-color: #ccc;
  border-radius: 9999px;
  cursor: pointer;
}

.angle-bracket {
  transition-duration: 300ms;
}

.select-container:hover .rotate-left {
  transform: rotate(-90deg);
}

.select-container:hover .rotate-right {
  transform: rotate(90deg);
}

.hidden-select {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
}
```

### Result

![solution demo](https://github.com/palmerusaf/blog/blob/main/01-Style-Select-Tag/solution-demo.png?raw=true)

## Conclusion

Using a div as a mask, along with positioning tricks, is much easier than trying to fight the browsers. Anyways, I hope you found this article helpful. Let me know what you think in the comments.
