---
title: CSS Animations and Transitions
length: 
tags: animation, transition, css
---

### Goals

By the end of this lesson, you will::

* Have a general understanding of CSS Transitions and Transforms
* Be familiar with the basic concepts and syntax and be able to implement them in your CSS

You might think you need to write a good bit of Javascript to incorporate animations in a website, but that's not the case! We can use good ol' CSS to make transitions and animations, no Javascript required.

This is surprising to many who think of CSS as simply a way to create layouts, but one of the great things about CSS animations is that the barrier of entry is lower than doing a similiar task with JS. 

In this lesson, we'll start to get familiar with CSS transitions and transforms. By the end of class, you'll be able to add these experience-enhancing elements to your CSS!


#### What are CSS Transitions?

CSS transitions allow property changes in CSS values to occur smoothly over a specified duration of time. They allow you to create dynamic effects without using any Javascript.

We trigger transition in many of the same ways we might trigger a Javascript action -- on hover, mouse click, focus, or changes to the element.

There are **specific properties** associated with transtions that let us set exactly how we want our transition to execute.


``transition-property`` lets us specify which CSS property (or properties) we are setting the transition on. This can be written to specify one CSS property, or all CSS properties. A full list of supported properties can be found [here](https://www.w3.org/TR/css3-transitions/#animatable-css).

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
* ease-in
* ease-out
* ease-in-out
* step-start
* step-end
* cubic-bezier

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

**You can take a look at this code live on [CodePen](http://codepen.io/LouisaBarrett/pen/pbggJK)**. Go ahead and play around with it! Try changing the property that's being targeted. Try adjusting the amount of time that the transition is executing over. It's important to note that not all properties are animatable. The full list of all the animatable properties we can use can be viewed [here](https://www.w3.org/TR/css3-transitions/#animatable-properties)

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

Great! We can make a simple transition, now let's try something a little more dynamic. Let's make something move across the screen. **You can check out this code on [CodePen](http://codepen.io/LouisaBarrett/pen/dXGpPo).**

In our HTML, let's make a div with a class of `.box`, and wrap it in another larger div with a class of `.container`.

```html
<div class="container">
  <div class="box"></div>
</div>
```

In our CSS, let's style these divs so we have something to work with:

```css
.container {
  border: 1px solid grey;
  height: 400px;
  width: 90%;
  margin: 0 auto;
  padding: 15px;
}

.box {
  background-color: yellow;
  border-radius: 30px;
  height: 300px;
  width: 25%;
}
```

Let's have the transition triggered when we hover over the outer `.container `rather than the inner `.box`. This will make it easier for us to trigger the transition and see the entire transiton play out. Let's add that `:hover` to our CSS:

```css
.container {
  border: 1px solid grey;
  height: 400px;
  width: 90%;
  margin: 0 auto;
  padding: 15px;
}

.box {
  background-color: yellow;
  border-radius: 30px;
  height: 300px;
  width: 25%;
}

.container:hover .box {
    background: green;
}
```

What this is doing is saying when we `:hover` on `.container` we want to change the background-color property on `.box`.

To make `.box` move, we'll need to change the margin on our `:hover` to push our `.box` over to the right side of the screen.

```css
.container:hover .box {
    background: green;
    margin-left: 75%;
}
```

Cool! But that doesn't look very good, does it? Transitions to the rescue! Let's add a `transition-duration` property to our `.box` class.

```css
.box {
  background-color: yellow;
  border-radius: 30px;
  height: 300px;
  width: 25%;
  transition-duration: 1s;
}
```

Remeber, putting the transition property directly on the `.box` class rather than the `:hover` means we will get our transition as it's triggered and as it's ending.

We can now go a step further and control the speed and duration of this transition with timing functions. We do this with the [`transition-timing-function` property](https://www.w3.org/TR/css3-transitions/#transition-timing-function-property).

We can do some intersting things with this property. Let's try a few out! Add the `transition-timing-function` to `.box`.

Let's start simple:

```css
.box {
  background-color: yellow;
  border-radius: 30px;
  height: 300px;
  width: 25%;
  transition-duration: 1s;
  transition-timing-function: ease;
}
```
When you ran that, what did you notice? It didn't really look any different, did it? That's because `ease` is actually the default, so the the transformation shouldn't have changed.

Let's try one that's a little more interesting! `steps` lets you assign a specific number of steps to the transition. Let's see what that looks like:

```css
.box {
  background-color: yellow;
  border-radius: 30px;
  height: 300px;
  width: 25%;
  transition-duration: 1s;
  transition-timing-function: steps(4, end);
}
```

All of these `transition-timing-function` properties are mapped to `cubic-bezier`. If you've used software to create vector graphics (like Adobe Illustrator) you're probably familiar with the bezier pen tool. And since all these timing function properties are mapped to it, we can also just write them ourselves! As the W3C descibes it:
"Specifies a [cubic-bezier curve](https://en.wikipedia.org/wiki/B%C3%A9zier_curve). The four values specify points P1 and P2 of the curve as (x1, y1, x2, y2). Both x values must be in the range [0, 1] or the definition is invalid. The y values can exceed this range."

Very simply put, it allows us to specify the speed and duration of our transition as it's happening. So we can set the starting speed, the speed during the middle, and the speed at the end. Lea Verou has a [great site](http://cubic-bezier.com/#.17,.67,.83,.67) to help you see how different specifications will impact your transition.

Let's try it out. We'll start with something very dramitic, so play around with it and see how different inputs change the transition:

```css
.box {
  background-color: yellow;
  border-radius: 30px;
  height: 300px;
  width: 25%;
  transition-duration: 1s;
  transition-timing-function: cubic-bezier(1, -1, 1, 5);
}
```

We can also delay when the transition begins with the `transition-delay` property. This lets us specify in seconds or miliseconds how long it should take for the tranistion to execute. Let's try it.

```css
.box {
  background-color: yellow;
  border-radius: 30px;
  height: 300px;
  width: 25%;
  transition-duration: 1s;
  transition-delay: 2s;
}
```

Now, we can clean up all these individual lines specificing our transition properties. The order in the shorthand is important, because the second time value specified will always be considered the `transition-delay`. Here's an example:

```css
.box {
  background-color: yellow;
  border-radius: 30px;
  height: 300px;
  width: 25%;
  transition: margin 1s cubic-bezier(1, -1, 1, 5) 0s;
}
```

#### What are CSS Transformations?

As defined by [Mozilla](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transforms/Using_CSS_transforms):
"By modifying the coordinate space, CSS transforms change the shape and position of the affected content without disrupting the normal document flow."

We implement transforms in much the same way that we implemented transitions: we use a set of CSS properties that allow us to apply linear transformations to HTML elements. Transitions include: rotation, skewing, and scaling.

#### Let's Try Some Transformations!

We'll use the same HTML:

```html
<div class="container">
  <div class="box"></div>
</div>
```

and let's use this as our CSS:

```css
.container {
  border: 1px solid grey;
  height: 400px;
  width: 90%;
  margin: 0 auto;
  padding: 15px;
}

.box {
  background-color: yellow;
  border-top: 5px solid red;
  height: 95px;
  width: 100px;
  -webkit-transform: rotate(45deg);
}
```

**Try it out in this [CodePen](http://codepen.io/LouisaBarrett/pen/rLxjVG).**

In this example, we see that `rotate` takes an argument that is the degrees of rotation we want. If we have a positive number here, it rotates clockwise. If we have a negative number, it rotates counter clockwise.

Try a few more approaches to `rotate` and see what they do.

```css
  -webkit-transform: rotate(.5turn);
```

```css
  -webkit-transform: rotate(.75turn);
```

Now for the fun part! To maximize the power of our transforms, we combine them with transitions.

Back in our CSS, let's add a transition to our `.box` add a `:hover` to our `.container`. Move our tranform into the block of CSS on `:hover` so that is what we trigger when we hover over our wrapping element:

```css
.container {
  border: 1px solid grey;
  height: 400px;
  width: 90%;
  margin: 0 auto;
  padding: 15px;
}

.box {
  background-color: yellow;
  border-top: 5px solid red;
  height: 95px;
  width: 100px;
  transition: 1s ease-in-out;
}

.container:hover .box {
  -webkit-transform: rotate(2turn);
}
```

Now that's much more like an animation!

#### Your Turn

Take a crack at implementing the scale and skewing transformations!






