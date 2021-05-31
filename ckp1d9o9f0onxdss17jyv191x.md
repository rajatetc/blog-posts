## 🎯 JS Interview Checklist - Part 1 (Basics)

Prepping for your next interview ❓ I have the perfect checklist for you. Go through this and you are ready to rock 💃

## 📝Prerequisites

- Basic knowledge of how the web works
- Familiar with HTML/CSS, JS (especially ES6+ syntax)

## 🧰 Array Methods

Most commonly asked: `map`, `filter`, `find`, `reduce`, `forEach`

 ### ❓ Examples of usage, solve a problem

```
// Return the words with more than 6 letters
const words = ['react', 'script', 'interview', 'style', 'javascript']

const ans = words.filter((word) => word.length > 6)

console.log(ans) // ['interview', 'javascript']

``` 
I recommend doing the exercise yourself first to test your knowledge.

Comment your solutions⬇️

Generally, a follow up to this: can you do it without the array method?


```
let newArr = []

for (let i = 0; i < words.length; i++) {
  if (words[i].length > 6) {
    newArr.push(words[i])
  }
}
console.log(newArr)
``` 

### ❓ Difference between map and forEach


- `map` returns a new Array, `forEach` doesn't

```
// Return a new array where even numbers are multiplied by 2 
let arr = [1, 2, 3, 4, 5, 6, 7]

function consoleEven(arr) {
  let data = arr.map((num) => (num % 2 === 0 ? num * 2 : num * 1))
  console.log(data)  // [1,  4, 3, 8, 5, 12, 7]
}
consoleEven(arr) 

```

```
function consoleEven(arr) {
  let data = arr.forEach((num) => (num % 2 === 0 ? num * 2 : num * 1))
  console.log(data) // undefined
}
consoleEven(arr)
```
- method chaining can be done in `map` but not `forEach`

```
// we are converting the new array back to original
function consoleEven(arr) {
  let data = arr
    .map((num) => (num % 2 === 0 ? num * 2 : num * 1))
    .map((item) => (item % 2 === 0 ? item / 2 : item / 1))
  console.log(data)
}

consoleEven(arr)
```
**Note: ** `map` and `forEach` don't mutate the original array

### ❓ Polyfill of map

This is an advanced concept. We will cover this in Part-2

## ✔️ var, let and const 

### ❓  Difference between, scope
![6-var-let-const-all-diff.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1621775840670/-wnr0JLxh.png)

### ❓  Output

```

var a = 3
var a = 4
let b = 3
let b = 4
const c = 3
const c = 4

console.log(a) // 4
console.log(b) // Syntax Error
console.log(c) // Syntax Error

``` 
**Note:** Good idea to know different types of error

## 🚩 Hoisting

JavaScript's default behavior of moving declarations to the top.

`function` and `var` declarations are hoisted

Note: `var` declaration is hoisted - not the value

### ❓  Output/Explain the error

```
function consoleNum() {
  console.log(num)
  var num = 10
}

consoleNum() // undefined

// Why? Also, why undefined & not error

// This is how runtime sees this
{
  var num
  console.log(num)
  num = 9
}

```

## ✔️ == vs ===

`==` converts the operand to the same type and then compares them

`===` depicts strict equality check. It checks for same type and same content

### ❓  Output


```
let a = null
let b

console.log(a == b) // true
console.log(a === b) // false

// why?

console.log(typeof a) // object
console.log(typeof b) // undefined
``` 
**Note:** Always a good practice to explain your answers.

## ✔️ this

To explain it properly will require another article. Here, I just list some key things.

`this` refers to the `object` that the function belongs to, in simpler terms, points to the owner of the function call (left of the dot)

Its value depends on how it is invoked.

### ❓  Implicit vs Explicit Binding

**Implicit binding** is when you invoke a function in an object using dot notation.


```
function myFunc() {
    console.log(this)     
  }
 
const obj = {
  bool: true,
  myFunc: myFunc,
}
``` 

**Explicit binding** is when you force a function to use a certain object as its `this`.

Ways to do that:
![call-bind-apply.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1622489263380/UwpR9Rscv.png)

### ❓  Output

```
const myData = {
  name: 'Rajat',
  city: 'Delhi',
  displayStay: function () {
    console.log(this.name, 'stays in', this.city)
  },
}
myData.displayStay()

// create an object yourData and try to use displayStay
const yourData = {
 name: 'name',
 city: 'city'
}

// answer
myData.displayStay.call(yourData)

``` 
**Note: ** For an arrow function, it depends on the lexical scope, that is to say, the outer function where the arrow function is declared.

## ✔️ Async and defer

Async and defer are `boolean` attributes which can be loaded along with the script tags. They are useful for loading external scripts into your web page.

### ❓ Difference between
🏢 Asked by big corporations like Amazon, Walmart, and Flipkart

Best explained through pictures:

![18-async-defer.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1621781371965/PciAdUTCL.png)
![19-async-defer.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1621781403795/VgIYFtP5T.png)
![20-async.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1621781415787/mJEkxqe_i.png)
![21-defer.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1621781428927/2nUaI8fjr.png)

If there are multiple scripts which are dependant on each other, use `defer`. Defer script are executed in the order which they are defined.

If you want to load external script which is not dependant on execution of any other scripts, use `async`. 

**Note:** Async attribute does not guarantee the order of execution of scripts.

## 💾Local and session storage 

### ❓ Difference between

**localStorage:** Data persists even after closing your session

**sessionStorage:** Data is lost when your session is over, ie, on closing the browser on the tab


```
// save
localStorage.setItem('key', 'value')
// get saved data
let data = localStorage.getItem('key')
// remove saved data
localStorage.removeItem('key')
// Same for sessionStorage
``` 

## ⏱️ Timers - setTimeout, setInterval, clearInterval

`setTimeout()` method calls a function or evaluates an expression after a specified number of milliseconds.

`setInterval()` does the same for specified intervals.

Finally, `clearInterval()` is used to stop the timer.

### ❓  Output

```
  console.log('Hello')
  setTimeout(() => {
    console.log('lovely')
  }, 0)
  console.log('reader')

  // output
  Hello
  reader
  lovely
``` 
A slightly trickier one:
```
  for (var i = 1; i <= 5; i++) {
    setTimeout(function () {
      console.log(i)
    }, i * 1000)
  }

// output
6
6
6
6
6
```
 Short explanation: when `setTimeout` comes again into the picture, the entire loop has run and value of ` i` has become 6

Now, let's say we want the outcome to be 1 2 3 4 5, what to do?

`var` ➡️ `let`

Why this will work?
`var` is globally scoped but `let` is locally scoped so for `let` a new `i` is created for every iteration.

If you had trouble solving these outputs - don't worry. Subscribe for Part-2 where we will cover the event loop and other advanced topics.

Shoutout to 🗣️ [Akansha](https://twitter.com/ch_akanksha) for an informative session @ [roc8](https://twitter.com/roc8HQ) that enabled this blogpost. Check her [page](https://www.instagram.com/javascript_interviews).

Share and comment if you found this helpful. 

PS I have some sick threads 🧵🔥 on [Twitter](https://twitter.com/rajatetc/status/1394858829851025417)