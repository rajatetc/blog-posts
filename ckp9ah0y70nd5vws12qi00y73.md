## 🎯 JS Interview Checklist - Part 2 (Advanced)

You have covered the basics ✅

Now, you are ready to impress the interviewer with some advanced concepts 👨‍🔬 

Let's get started.

If you haven't read Part-1: https://rajatgupta.xyz/js-interview-1

## 📚 Polyfills
❓ Most commonly asked: map, bind


> A polyfill is a piece of code (usually JavaScript on the Web) used to provide modern functionality on older browsers that do not natively support it.

- Let's implement it for `map`

```
// this - array
// this[i] - current value
Array.prototype.myMap = function (cb) {
  var arr = []
  for (var i = 0; i < this.length; i++) {
    arr.push(cb(this[i], i, this))
  }
  return arr
}

const arr = [1, 2, 3]
console.log(arr.myMap((a) => a * 2)) // [2, 4, 6]
``` 

- `bind`


```
let name = {
  first: 'Rajat',
  last: 'Gupta',
}
let display = function () {
  console.log(`${this.first} ${this.last}`)
}

Function.prototype.myBind = function (...args) {
  // this -> display
  let obj = this
  return function () {
    obj.call(args[0])
  }
}

// let displayMe = display.bind(name)
let displayMe = display.myBind(name)

displayMe() // Rajat Gupta
``` 
But this is the basic implementation, suppose we have parameters in our display & displayMe function

```
let display = function (city, country) {
  console.log(`${this.first} ${this.last} from ${city}, ${country}`)
}

Function.prototype.myBind = function (...args) {
  let obj = this
  // get the args except the first one
  params = args.slice(1)
  return function (...args2) {
    obj.apply(args[0], [...params, ...args2])
  }
}

let displayMe = display.myBind(name, 'Delhi')
displayMe('India') // Rajat Gupta from Delhi, India
``` 
## ➰ Event Loop

A very ❗important topic to understand asynchronous behavior. 

Instead of providing a half-baked explanation here,  I recommend watching this video if you haven't already:

%[https://youtu.be/8aGhZQkoFbQ]


## 🔒 Closures ❗important  
❓ Explain, output Q, advantages, disadvantages

You have probably used it without even realizing it.

This section will have a lot of fancy words - so bear with me. We will cover them one by one.

> Function bundled together with its lexical environment forms a closure 

Okay, what is lexical environment❓

It is essentially the surrounding state - the **local memory** along with the lexical environment of its parent.

Whaaat? 🤯 I know it's a bit of a doozy. Let's understand it with an example.


```
function x() {
  var a = 7
  function y() {
    console.log(a)
  }
  return y
}

var z = x()
console.log(z) // [Function: y]
z()
``` 
When x is invoked, y is returned. Now, y is waiting to be executed. Kind of like a loaded gun waiting to be shot! 🔫

So, when we finally invoke z - y is invoked. Now, y has to log `a` so it first tries to find 🔍 it in the **local memory** but it's not there. It goes to its parent function. It finds `a` there. 

Voila❗There you have it - this is closure. 

Even when functions are returned (in the above case y) they still remember their lexical scope (where it came from)

Totally, unrelated quote for kicks 👻:
> They may forget what you said - but they will never forget how you made them feel - Carl W. Buehner

I swear the rest of the article is legit 🤞  Keep reading.


### Advantages 😎

- Currying

```
let add = function (x) {
  return function (y) {
    console.log(x + y)
  }
}

let addByTwo = add(2)
addByTwo(3)
``` 
- Data Hiding/Encapsulation

Suppose, you want to create a counter application. Every time, you call it - the count increases by 1. But you don't want to expose the variable outside the function. How to do it? 

You guessed it - closure❗

```
function Counter() {
  var count = 0
  this.incrementCount = function () {
    count++
    console.log(count)
  }
}

console.log(count) // Error: count is not defined
var adder = new Counter()
adder.incrementCount() // 1
``` 

### Disadvantages 😅

- Overconsumption of memory or memory leaks can happen. 

For example, the closed-over-variable will not be garbage collected. As even if the outer function has run, the returned inner function still has a reference to the closed-over-variable.

**Note: ** Garbage collector basically removes unused variables from the memory automatically. 

## 🤝Promises ❗important
❓ Syntax, explanation, output Q

Again, a *very* *very* important topic.

> The Promise object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

It is in one of these three states: 

- pending: initial state, neither fulfilled nor rejected
- fulfilled: operation was completed successfully
- rejected: operation failed

```
const promise = new Promise((resolve, reject) => {
  let value = true;
  if (value) {
    resolve("hey value is true");
  } else {
    reject("there was an error, value is false");
  }
});

promise
  .then((x) => {
    console.log(x);
  })
  .catch((err) => console.log(err));
``` 
**Note:** `resolve` and `reject` are just conventional names. Call it pizza🍕  if you like

Instead of `then/catch` - we can also use `async/await`

```
async function asyncCall() {
  const result = await promise
  console.log(result)
}

asyncCall()
``` 

One of the advantages of promises is that it is a much cleaner syntax. Earlier, it used to be a [callback hell](http://callbackhell.com/) 🌋

Now now, there is a lot more than this to Promises. Covering it in depth will require a separate blog post. Let me know in the comments if you want that.


## 👪 Prototypes, Prototypal Inheritance
❓ Syntax, explanation

You may have noticed the keyword  `prototype` from the polyfill example.

From the emoji - you might think this is like the inheritance in other languages like `C++`. But it's not.


> Whenever we create anything (object, function) in JS - JS Engine automatically attaches that anything with some properties and methods

All this comes via `prototypes`

`__proto__`  is the object where JS is putting it all

Let's take some examples. Fire up your consoles!

```
let arr = ['Rajat', 'Raj']
console.log(arr.__proto__.forEach)
console.log(arr.__proto__) // same as Array.prototype
console.log(arr.__proto__.__proto__) // same as Object.prototype
console.log(arr.__proto__.__proto__.__proto__) // null
``` 
All this is called a `prototype chain`

We can do the same with objects and functions as well. 

We will always find `Object.prototype` behind the scenes. That's why you may have heard - everything in JS is nothing but an object 🤯

### Prototypal Inheritance

```
let object = {
  name: 'Rajat',
  city: 'Delhi',
  getIntro: function () {
    console.log(`${this.name}, ${this.city}`)
  },
}

let object2 = {
  name: 'Aditya',
}
``` 

**Note:** Don't modify prototypes this way. It's just for understanding. The right way to do it: https://javascript.plainenglish.io/how-prototypal-inheritance-works-in-javascript-and-how-to-convert-it-to-class-based-inheritance-632e31e6350d

```
object2.__proto__ = object
``` 
By doing this, object2 gets access to the object's properties. So, now we can do:

```
console.log(object2.city)
```
This is **prototypal inheritance**.

Coming back to the polyfill of `bind` from before:

```
Function.prototype.myBind = function () {
  // code
}
// now we can access this method whenever we create a new function
function a(){
 // code
}

console.log(a.__proto__) // will have myBind method
``` 
## ⚡Performance Optimization 

- Debouncing
- Throttling
- Caching 
- Code Splitting
- Bundling, Minification
- Server-side rendering

**Note:** Generally not asked to freshers 👶 but good to know 📝

Let's cover debouncing and throttling. 

## ⛹️‍♂️Debouncing 

Another favorite of interviewers.  

Let's understand it by creating a search bar.

**Demo:** https://codesandbox.io/s/debounce-input-field-o5gml

Create a simple input field in `index.html`
```
<input type="text" id="text" />
``` 

Now, `index.js`. Don't forget to add it to `index.html`
```
const getData = (e) => {
  console.log(e.target.value);
};
const inputField = document.getElementById("text");

const debounce = function (fn, delay) {
  let timer;
  return function () {
    let context = this;
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(context, arguments);
    }, delay);
  };
};

inputField.addEventListener("keyup", debounce(getData, 300));

``` 
First, we have selected the input and added an `event listener` to it. Then we created a debounce function which takes a callback function and delay.

Now, inside the debounce function we create a timer using `setTimeout`. Now, this timer's job is to make sure - the next call for `getData` only happens after 300 ms. This is what debouncing is.

Also, we use `clearTimeout` to remove it.  Don't want too many of them hanging out there taking up memory space!

Phew! Lots of theory. Let's do a fun challenge. You must have seen the countdown before a game starts (it goes like 10, 9, 8, .... with some delay in between). Try to write a program for it.

Answer
```
let count = 10

for (let i = 0; i < 10; i++) {
  function timer(i) {
    setTimeout(() => {
      console.log(count)
      count--
    }, i * 500)
  }
  timer(i)
}
``` 
Were you able to solve it? Did it differently? Let me know your solution.

## 🛑 Throttling

Let's take an example again. Suppose, on every window resize event - we call an expensive function. Now, we want it such that the expensive function will only be executed once in the given time interval. This is what throttling is.

Create an`index.html` and an `index.js` with the following code:

```
const expensive = () => {
  console.log('expensive')
}

const throttle = (fn, limit) => {
  let context = this
  let flag = true
  return function () {
    if (flag) {
      fn.apply(context, arguments)
      flag = false
    setTimeout(() => {
      flag = true
    }, limit)
       }
  }
}
const func = throttle(expensive, 2000)
window.addEventListener('resize', func)

``` 
Almost the same as debouncing. The key difference is the `flag` variable. Only, when it's true - we are invoking the callback function. And it is set to `true` inside the `setTimeout` . So the value is `true` only after the desired time limit.

### So, what's the difference between debounce and throttling❓

Let's take the search bar 🔍 example from above. When we are debouncing the input field - we are saying that only fetch the data when the difference between two `keyup` events is at least 300 ms.

In the case of throttling, we make a function call only after a certain period of time. Suppose, you are searching for an encyclopedia in the search bar. Say, the first call is made on `e` and it took us 300 ms to reach `p`. The next call will be made then only. All the events in between will be ignored. 

So, to summarize, debouncing - when the difference between two `keyup` events is 300 ms and throttling - when the difference between two function calls is 300 ms. Basically, the function is called after a certain interval of time.

And we are doneee 🏁

I hope this article was useful. Do like, share, and comment 👇

Until next time 👋

## 🗃️ References:
- MDN Docs: https://developer.mozilla.org/en-US/
- Akshay Saini: https://www.youtube.com/channel/UC3N9i_KvKZYP4F84FPIzgPQ
- Coding Addict: https://www.youtube.com/channel/UCMZFwxv5l-XtKi693qMJptA