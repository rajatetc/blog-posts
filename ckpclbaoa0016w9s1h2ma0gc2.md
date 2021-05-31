## 💡Know The Differences Between Event Capturing, Bubbling & Delegation  in JS

Do you get confused 😵 about the order in which event listeners are invoked when you click on an element? Then this article is for you.

Also, this is a hot 🔥 question in JavaScript interviews.

## 📝Prerequisites
-  Basic HTML/CSS
-  Familiar with DOM Manipulation in JavaScript

When we want to modify the DOM - the normal flow of things is like this:

Select an `element` -> `addEventListener('event', callback fn)` -> What to do

Things get a little complicated when you have nested elements like:

`<div>` -> `<li>` -> `<p>`

If you attach an event listener to every element - what will be the order of execution? 

Before we answer that, let's cover what is an **event object**

## 👨‍🏫Basics

Whenever we use an event handler function, a parameter is automatically passed to it. It contains some extra information. Generally specified as `event`, `evt` or `e`. This is the **event object**.

One of the most useful properties of an event object is `target`. 

> The `target` property of the event object is always a reference to the element the event occurred upon

Just remember this for now. It will make more sense when we take the examples below.

Let's come back to `addEventListener()` for a bit. You can actually pass a third argument to it - `useCapture`.

It's a boolean value. By default, it is set to `false` meaning browsers run the bubbling phase, basically, event bubbling is used. You can set it to `true` for running the capturing phase.

## 🎈 Event Bubbling 

- In the bubbling phase, browsers run the `event handler` on the element first (if it has one)

- Then it moves to the next immediate ancestor (parent) element and does the same thing, and then the next until it reaches the `<html>` element

Let's understand it better with the help of an example.

**Demo:** https://codesandbox.io/s/event-bubbling-s4bbo?file=/src/index.js

Create an `index.html` file with three `divs` like this:

```
<!DOCTYPE html>
<html>
  <head>
    <title>Event Bubbling</title>
    <meta charset="UTF-8" />
  <style>
    div {
      min-width: 100px;
      min-height: 100px;
      padding: 30px;
      border: 1px solid black;
    }
  </style>
</head>
<body>
  <div id="grandparent">
    <div id="parent">
      <div id="child"></div>
    </div>
  </div>
  <body>
    <script src="src/index.js"></script>
  </body>
</html>
```
Select the elements and add a `click` event listener with a simple log function in `index.js`:

```
document.querySelector("#grandparent").addEventListener("click", () => {
  console.log("grandparent clicked");
});
document.querySelector("#parent").addEventListener("click", () => {
  console.log("parent clicked");
});
document.querySelector("#child").addEventListener("click", () => {
  console.log("child clicked");
});
```

Now, click on the `div` with `#child` and check your console. It will be:

```
child clicked 
parent clicked 
grandparent clicked
```

If you click on `div` with `#parent`:

```
parent clicked 
grandparent clicked
```

Notice the order of execution. See how it *bubbles* up.

## ⬇️ Event Capturing

Also known as **Event Trickling** is essentially the opposite of Event Bubbling.

Outer-most ancestor -> next element -> selected element

In the same `index.js`, give the third argument as `true` to all `three` elements like this:

```
document.querySelector('#grandparent').addEventListener(
  'click',
  () => {
    console.log('grandparent clicked')
  },
  true
)
```

Now, when you click on the child element, the console will be like this:

```
grandparent clicked 
parent clicked 
child clicked 
```

Now, let's make it a little trickier, set the parent element to `false` and keep the others as `true`. What will be the output when you click on the child element?

```
grandparent clicked 
child clicked 
parent clicked
```
First, we have the capturing phase. `grandparent` is set to `true` so it is logged. `parent` is `false` so it is skipped. `child` is logged.

Now, in the bubbling phase - `parent` is logged.

❓ for you: What will happen if we put the child element to `false` as well? Comment your answer 👇

### 🛑e.stopPropagation()

Now, all this bubbling/capturing is a very expensive task (in terms of performance). More on this later when we cover **event delegation**

Also, it gets annoying at times.

How to stop it?

Remember, the **event object** from before? We can call a method on it - namely:
`stopPropagation`

So, if we write the child element like this:

```
document.querySelector('#child').addEventListener(
  'click',
  (e) => {
    console.log('child clicked')
    e.stopPropagation()

  },
  false
)
``` 

Can you guess what will happen when we click on it? Only `child clicked` will be logged.

## ✈️ Event Delegation

Suppose, you have a large application (like an e-commerce store) having a lot of events. Do you think it's a good idea to attach event listeners to every element? 

It's not. It will consume a lot of memory. Not to mention the extra lines of code.

An efficient way of dealing with this problem is **event delegation**

Event delegation takes advantage of event bubbling. The idea is that if you want some code to run for any one of a large number of child elements, you set the event listener on the parent and have the events bubble up.

Let's understand this with the help of an example.

**Demo:** https://codesandbox.io/s/event-delegation-loyfw?file=/src/index.js

Create a simple unordered list like this in `index.html`:

```
    <div>
      <ul id="category">
        <li id="oranges">oranges</li>
        <li id="apples">apples</li>
        <li id="bananas">bananas</li>
      </ul>
    </div>
``` 

Now, in `index.js`  - only attach an event listener to `<ul>` element:

```
document.querySelector('#category').addEventListener('click', (e) => {
  console.log(e.target)
  }
})
``` 
Notice `e.target` - as covered earlier, it is a reference to the element on which event happens. Now, when you will click on the `<li>` with `#oranges`. It will log:

```
<li id="oranges">oranges</li>
```

Finally, let's cover the pros and cons of using event delegation.

### ➕Pros

- As discussed earlier, with event delegation - we have fewer event listeners and we save memory. Our applications are optimized.
- Less code as we are not having an event handler on every child
- It is easier to do DOM manipulation. Suppose, we are doing infinite scroll in our app.  Now, we don't have to attach event listeners to every new element. As bubbling will happen and we can just have it on the parent.

### ➖Cons

- Not all event gets bubbled up. Example: `resize`, `focus`, and `blur`.
-  Remember `e.stopPropagation`? If we use that anywhere in our code, bubbling won't happen from that point on.

And we are done 🏁

If you found this helpful - like, comment, and share.

## 📚References

Akshay Saini: https://www.youtube.com/channel/UC3N9i_KvKZYP4F84FPIzgPQ

MDN: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events