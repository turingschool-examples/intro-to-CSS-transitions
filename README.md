---
title: CSS Transitions and Transformations
length:
tags: animation, transition, transformations, css
---

### Goals

By the end of this lesson, you will:

* Have a general understanding of CSS Transitions, Transforms, and Animations
* Be familiar with the basic concepts and syntax and be able to implement them in your CSS

You might think you need to write a good bit of Javascript to incorporate animations in a website, but that's not the case! We can use good ol' CSS to make transitions and animations, no Javascript required.

This is surprising to many who think of CSS as simply a way to create layouts, and one of the great things about CSS animations is that the barrier of entry is lower than doing a similar task with JS.

In this lesson, we'll start to get familiar with CSS transitions, transforms, and animations. By the end of class, you'll be able to add these experience-enhancing elements to your CSS!


### What are CSS Transitions?

CSS transitions allow property changes in CSS values to occur smoothly over a specified duration of time. They allow you to create dynamic effects without using any Javascript.

The most common way to trigger a transition is with a `:hover` action.

There are **specific properties** associated with transitions that let us set exactly how we want our transition to execute.


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


``transition-duration`` sets the amount of time the transition will take to execute. We specify the number or seconds, or milliseconds, the transition should take to complete. Setting the duration to one second looks like this:

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


``transition-timing-function`` defines how a transition will proceed over it's duration and allows the transition to change speed during it's course. This property accepts predefined keyword values, which you can read about in-depth in the W3C definition of them [here](https://www.w3.org/TR/css3-transitions/#transition-timing-function-property), and include:

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
}

div:hover {
    background-color: green;
}
```

You can also chain properties that you want to transition. Let's change the `border-radius` at the same time as the `background-color`, and set them to different duration speeds.

```css
div {
    background-color: yellow;
    border-radius: 30px;
    height: 300px;
    width: 300px;
    margin: 0 auto;
    transition-property: background-color, border-radius;
    transition-duration: 2s, 4s;
}

div:hover {
    background-color: green;
    border-radius: 50%;
}
```

Since we really are simply animating all the animatable properties here, we can write it a more concise way by setting the `transition-property` to `all`, but note that when we do this we lose the different transition durations we applied when we were explicitly targeting our CSS properties:

```css
div {
    background-color: yellow;
    border-radius: 30px;
    height: 300px;
    width: 300px;
    margin: 0 auto;
    transition-property: all;
    transition-duration: 2s, 4s;
}

div:hover {
    background-color: green;
    border-radius: 50%;
}
```

And since `transition-property: all` is the default, we can actually just remove that line all together! And, since we've lost our targeted `transition-duration`, we can go ahead and adjust that as well:

```css
div {
    background-color: yellow;
    border-radius: 30px;
    height: 300px;
    width: 300px;
    margin: 0 auto;
    transition-duration: 4s;
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

Let's have the transition triggered when we hover over the outer `.container `rather than the inner `.box`. This will make it easier for us to trigger the transition and see the entire transition play out. Let's add that `:hover` to our CSS:

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

Remember, putting the transition property directly on the `.box` class rather than the `:hover` means we will get our transition as it's triggered and as it's ending.

We can now go a step further and control the speed and duration of this transition with timing functions. We do this with the [`transition-timing-function` property](https://www.w3.org/TR/css3-transitions/#transition-timing-function-property).

We can do some interesting things with this property. Let's try a few out! Add the `transition-timing-function` to `.box`.

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

All of these `transition-timing-function` properties are mapped to `cubic-bezier`. If you've used software to create vector graphics (like Adobe Illustrator) you're probably familiar with the bezier pen tool. And since all these timing function properties are mapped to it, we can also just write them ourselves! As the W3C describes it:
"Specifies a [cubic-bezier curve](https://en.wikipedia.org/wiki/B%C3%A9zier_curve). The four values specify points P1 and P2 of the curve as (x1, y1, x2, y2). Both x values must be in the range [0, 1] or the definition is invalid. The y values can exceed this range."

Very simply put, it allows us to specify the speed and duration of our transition as it's happening. So we can set the starting speed, the speed during the middle, and the speed at the end. Lea Verou has a [great site](http://cubic-bezier.com/#.17,.67,.83,.67) to help you see how different specifications will impact your transition.

Let's try it out. We'll start with something very dramatic, so play around with it and see how different inputs change the transition:

```css
.box {
  background-color: yellow;
  border-radius: 30px;
  height: 300px;
  width: 25%;
  transition-duration: 1s;
  transition-timing-function: cubic-bezier(1, -1, 1, .5);
}
```

We can also delay when the transition begins with the `transition-delay` property. This lets us specify in seconds or milliseconds how long it should take for the transition to execute. Let's try it.

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

#### Your Turn

Time to practice! Make 4 divs inside a wrapping element. When the wrapping element is hovered on, apply different transitions to all 4 internal divs using `transition-delay` so the transition execute at different times. Make them move, change colors, change borders, go nuts. Use this block of code as a starting point:

```css
div .a { transition-delay: 0s; }
div .b { transition-delay: 1s; }
div .c { transition-delay: 2s; }
div .d { transition-delay: 3s; }
```


### What are CSS Transformations?

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

Back in our CSS, let's add a transition to our `.box` add a `:hover` to our `.container`. Move our transform into the block of CSS on `:hover` so that is what we trigger when we hover over our wrapping element:

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

We can also change where the origin of the transform is, with the `transform-origin` property. This lets you control the X and Y axis that the transformation is originating from. You can change this by specifying a different origin value.

For example, `transform-origin: 50% 50%` puts the origin at 50% of the X axis and 50% of the Y axis, which is right in the middle of the element you are transforming. `transform-origin: 100% 100%` puts the origin at 100% of the X and Y axis which is the lower right corner.

Let's try adding it to our code:

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
  -webkit-transform-origin: 100% 100%;
}
```

You can also use position key words like `top`, `right`, `bottom`, and `left`.

Try adjusting the `transform-origin` value numbers and see what happens!


#### Your Turn

Take a crack at implementing the [scale](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/scale) and [skew](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/skew) transformations!


### What are CSS Animations

For more involved movement, we can use CSS animations rather than transitions and transformations. What's the difference? A transition is typically a state change that goes from A to B (like a `:hover` state), while an animation may have many stages from A to B to C to D.

While there are many similar concepts used in transitions/transformations and animations, the biggest difference is that animations use `@keyframes`, the CSS rule where we write out the sequence of our animation. The `@keyframes` rule can be thought of as a timeline where we define the stages of our animation with each stage having it's own CSS declaration.

It's important to note that `@keyframes` must be bound to a selector -- this is how it knows where to apply the animation styles you've defined.

#### Keyframes

A `@keyframes` has the following properties:

* A name that we can reference when we bind it to our selector
* Stages from 0% to 100%
* CSS styles to control the changes and styling you want applied in each stage

Together, this looks like:

```CSS
@keyframes testAnimation {
  0% {
    background-color: yellow;
  }
  100% {
    background-color: aqua;
  }
}
```

Which can also be written using "from" and "to" rather than 0% - 100%:

```CSS
@keyframes testAnimation {
  from {
    background-color: yellow;
  }
  to {
    background-color: aqua;
  }
}
```

And just like that, we've defined the stages of our keyframes! In this case, we'll be moving from yellow to aqua. Read more about `@keyframes` in the [W3C spec](https://www.w3.org/TR/css3-animations/#keyframes).

#### Animation properties

Like transitions, there are specific `animation` properties we can use when we call `@keyframes` and a single animation can have more than one property applied to it.

You'll find many of these to be familiar if you've played around with transitions:

* `animation-name: name-of-keyframe` is how we call our `@keyframe` from within our CSS selector, and it's the only property that you _must_ use. It's what hooks up our animation.

* `animation-duration` indicated how long our animation should take to execute.

* `animation-timing-function` works just the same way as `transition-timing-function` does, it sets the speed of our animation using pre-set functions or your own custom `cubic-bezier` function.

* `animation-delay` sets how long it should be before our animation starts

* `animation-iteration-count` indicates how many times the animation will iterate through the stages set in `@keyframes`

* `animation-direction` allows you to change the direction of the animation loop direction, switching from start to end, to end to start, or both.

* `animation-fill-mode` indicates which styles will be applied to the element when our animation is finished (these include none, forwards, backwards, or both)

Let's take a look at what that looks like in our CSS:

```CSS
selector {
  animation-name: testAnimation;
  animation-duration: 4s;
  animation-delay: 1s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  animation-direction: alternate;
}
```

Once you get a handle on all the different properties and what they do, you can also write them in shorthand:

```CSS
selector {
  animation: testAnimation 4s 1s infinite linear alternate;
}
```

And with that, we've called the keyframe rule for `testAnimation` in our selector (this could be a `div`, a class, and id -- any selector you want).

#### Vendor Prefixes

CSS Animations is still a W3C working draft, which means that we still need to use vendor prefixes to help us minimize buggy behavior across browsers. We use the usual prefixes:

* Chrome & Safari: `-webkit-`
* Firefox: `-moz-`
* Opera: `-o-`
* Internet Explorer: `-ms-`

Setting these on your selector looks like this:

```CSS
selector {
  -webkit-animation: testAnimation 4s 1s infinite linear alternate;
  -moz-animation: testAnimation 4s 1s infinite linear alternate;
  -ms-animation: testAnimation 4s 1s infinite linear alternate;
  -o-animation: testAnimation 4s 1s infinite linear alternate;
  animation: testAnimation 4s 1s infinite linear alternate;
}
```

And your `@keyframes` would look like this:

```CSS
@-webkit-keyframes testAnimation  { /* define styles here */ }
@-moz-keyframes testAnimation  { /* define styles here */ }
@-ms-keyframes testAnimation  { /* define styles here */ }
@-o-keyframes testAnimation  { /* define styles here */ }
@keyframes testAnimation  { /* define styles here */ }
```

For experimenting in CodePen, you can get away with not using prefixes, but if you want to actually use an animation in an app or website be sure to include them.

#### Combining Animations

It's also possible to add more than one animation to a selector. We do this using a comma to separate the two.

It looks like this in our selector:

```css
.element {
  animation: testAnimation 4s 1s infinite linear alternate,
             testRotate 4s 1s infinite linear alternate;
}
```

And in our `@keyframes` we simply define two separate, appropriately names keyframe rules:

```CSS
@keyframes testAnimation  {
  from {
    background-color: yellow;
  }
  to {
    background-color: aqua;
  }
}

@keyframes testRotate {
  to {
    transform: rotate(45deg);
  }
}
```

#### Putting It Together

Let's try this out! Open up a new CodePen and let's make a shape that changes color and shape.

We'll start with our HTML selector:

```HTML
<div></div>
```

Yup. That's right, for this simple example all we need is a div to manipulate in our HTML. On to the CSS!

Let's start with setting up our basic styles on our div. We'll put a width, height, background color on it, and then center it so it looks nice.

```CSS
div {
  background: yellow;
  height: 200px;
  width: 200px;
  margin: 100px auto 0;
}
```

Next, let's add our `@keyframe` rule. We'll keep this simple and just have two stages:

```CSS
@keyframes testAnimation {
  0% {
    transform: rotate(360deg);
    border-radius: 50% 0 50% 0;
  }
  100% {
    background-color: aqua;
    border-radius: 0 50% 0 50%;
  }
}
```

Let's talk through what we've done here: We set a border-radius on the top left and bottom right corners in the first stage, and then in the second stage we move the border-radius to the top right and bottom left corners as well as changing the background color to aqua. We also added a transform to the first stage to rotate our shape to make it a little more dynamic.

Hmm. That's not doing anything. How annoying. Why is that?

Well, we haven't called our `@keyframe` in our selector yet! That's an easy fix. We'll use the verbose format for now, so it's easier to see exactly what animation properties we're using. Update your `div` styles:

```CSS
div {
  background: yellow;
  height: 200px;
  width: 200px;
  margin: 100px auto 0;

  animation-name: testAnimation;
  animation-duration: 3s;
  animation-delay: 0;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  animation-direction: alternate;
}
```

And with that, you've made a CSS animation! Check out the final solution [here](http://codepen.io/LouisaBarrett/pen/zKOovv).

#### Your Turn

Make a 4-stage animation. Experiment!
