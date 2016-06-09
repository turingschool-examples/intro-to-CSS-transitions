---
title: CSS Animations and Transitions
length: 
tags: animation, transition, css
---

### Goals

By the end of this lesson, you will know/be able to:

* Have a general understanding of CSS Transitions and Transforms
* Be familiar enough with the basic concepts and syntax that you can implement them in your CSS


### Structure

You might think you need to write a good bit of Javascript to incorporate animations in a website, but that's not the case! We can use good ol' CSS to make transitions and animations, no Javascript required.

This is surprising to many who think of CSS as simply a way to create layouts, but one of the great things about CSS animations is that the barrier of entry is lower than doing a similiar task with JS. 

In this lesson, we'll start to get familiar with CSS transitions and transforms. By the end of class, you'll be able to add these experience-enhancing elements to your CSS!

#### What are CSS Transitions?

CSS transitions allow property changes in CSS values to occur smoothly over a specified duration of time. They allow you to create dynamic effects without using any Javascript.

We trigger transition in many of the same ways we might trigger a Javascript action -- on hover, mouse click, focus, or changes to the element.

There are **specific properties** associated with transtions that let us set exactly how we want our transition to execute.

``trasition-property`` lets us specify which CSS property (or properties) we are setting the transition on. This can be written to specify one CSS property, or all CSS properties. A full list of supported properties can be found [here](https://www.w3.org/TR/css3-transitions/#animatable-css).

It looks like this when we specify one CSS property:

```css
div {
    transition-property: background-color;
}
```

And like this when we want to transition all the CSS properties (this also happens to be the default):

```css
div {
    transition-property: all;
}
```

``transition-duration`` sets the amount of time the transition will take to execute. We specify the number or seconds, or miliseconds, the transition should take to complete. Setting the duration to one second looks like this:

```css
div {
    transition-duration: 1s;
}
```

``transition-delay`` is how long it will take to begin the transition from the moment it has been triggered. Setting a series of transitions with delays ranging from zero seconds to three seconds looks like this:

```css
div .a { transition-delay: 0s; }
div .b { transition-delay: 1s; }
div .c { transition-delay: 2s; }
div .d { transition-delay: 3s; }
```

``transition-timing-function`` defines how a transition will proceed over it's duration and allows the transition to change speed during it's course. This property accepts predefined keyowrd values, which you can read about indepth in the W3C definition of them [here](https://www.w3.org/TR/css3-transitions/#transition-timing-function-property), and include:

* ease
* linear
* ease-in\
* ease-out
* ease-in-out
* step-start
* step-end
* cubic-bezier (this one is a little tricky -- try it out and see how it works [here](http://cubic-bezier.com/#.17,.67,.83,.67))

Setting the timing function to `ease` looks like this:

```css
div { 
    transition-timing-function: ease;
}
```

#### Let's Try Some Transitions!

We'll start by writing some simple HTML so our CSS has something to work with. An empty div will be just fine --  we'll just put a width, height, and background color on it to give us something to play with.

```html
<!doctype html>
<html>
<head>
    <title>CSS Transitions</title>
</head>
<body>
    <div></div>
</body>
</html>
```

Time to write our styles. Remember, we need a pseudo class for our transition to work on. Let's use ``:hover``.

```css
div {
    background-color: yellow;
    border-radius: 30px;
    height: 300px;
    width: 300px;
    margin: 0 auto;
}

div:hover {
    background-color: green;
    transition-property: background-color;
    transition-duration: 2s;
    transition-timing-function: ease;
}
```

You can take a look at this code live on [CodePen](http://codepen.io/LouisaBarrett/pen/pbggJK). Go ahead and play around with it! Try changing the property that's being targeted. Try adjusting the amount of time that the transition is executing over. It's important to note that not all properties are animatable. The full list of all the animatable properties we can use can be viewed [here](https://www.w3.org/TR/css3-transitions/#animatable-properties)

Hmm. Something isn't quite right with this example. When we trigger the transition, the duration and timing function properties kick in and we have a nice smooth transition, but when we move our cursor off it changes back to the original state very abruptly. That's not what we want! But there's good news, it's an easy fix. In the Codepen, move the CSS transition properties from `div:hover` into `div`. This change let's us trigger the transitions when we start the transition and again as it's transitioning back to it's original state. The code looks like this:

```css
div {
    background-color: yellow;
    border-radius: 30px;
    height: 300px;
    width: 300px;
    margin: 0 auto;
    transition-property: background-color;
    transition-duration: 2s;
    transition-timing-function: ease;
}

div:hover {
    background-color: green;
}
```

You can also chain properities that you want to transition. Let's change the `border-radius` at the same time as the `background-color`, and set them to different duration speeds.

```css
div {
    background-color: yellow;
    border-radius: 30px;
    height: 300px;
    width: 300px;
    margin: 0 auto;
    transition-property: background-color, border-radius;
    transition-duration: 2s, 4s;
    transition-timing-function: ease;
}

div:hover {
    background-color: green;
    border-radius: 50%;
}
```

Since we really are simply animating all the animatable properties here, we can write it a more consise way by setting the `transition-property` to `all`:

```css
div {
    background-color: yellow;
    border-radius: 30px;
    height: 300px;
    width: 300px;
    margin: 0 auto;
    transition-property: all;
    transition-duration: 2s, 4s;
    transition-timing-function: ease;
}

div:hover {
    background-color: green;
    border-radius: 50%;
}
```

And since `transition-property: all` is the default, we can actually just remove that line all together!

```css
div {
    background-color: yellow;
    border-radius: 30px;
    height: 300px;
    width: 300px;
    margin: 0 auto;
    transition-duration: 2s, 4s;
    transition-timing-function: ease;
}

div:hover {
    background-color: green;
    border-radius: 50%;
}
```

