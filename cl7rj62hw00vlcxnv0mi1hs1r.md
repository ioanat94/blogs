## Core JavaScript: Var vs. Let vs. Const

## About the series

Core JavaScript is a series I'm writing that covers, as the name suggests, some of the core principles of JavaScript. It originally started as study or reference material for myself, but I decided to share it with the community in the hopes that it will prove useful for others. 

This series is intended for beginner JavaScript developers, or more experienced developers in need of a refresher. I have a few topics planned out already, but I would love to hear from you if there are any topics in particular you would be interested to read about!

---

In this article, I will go over the different ways of declaring variables in JavaScript, their characteristics (redeclarability, reassignability, scope and hoisting), and when to use which. At the end there will be a few exercises to practice the concepts I talked about.

Below is a quick summary of the main characteristics of each variable declaration:

|       | Redeclarable | Reassignable |       Scope       |         Hoisting         |
| ----- | :----------: | :----------: | :---------------: | :----------------------: |
| var   |      ✔       |      ✔       | global / function |   hoisted, initialized   |
| let   |      ❌       |      ✔       |       block       | hoisted, not initialized |
| const |      ❌       |      ❌       |       block       | hoisted, not initialized |



## Var

Before ES6, `var` was the only option for declaring variables in JavaScript, but it came with a few problems. For example, `var` variables can be redeclared, which means that doing something like this is perfectly valid:



```js
var name = 'Steve';
var name = 'Chris';
```



This is not an issue if you're doing it intentionally. The problem arises when you may not be aware that a certain variable has been declared already. This can lead to unexpected outputs, errors, bugs and headaches.

Another characteristic of `var` variables is that they can be reassigned, which means you can freely change their value after they've been declared.



```js
var age = 28;
age = 30;
```



In terms of scope, `var` variables are either in the global scope (if they have been declared outside of a function) or in the function scope (if they have been declared inside of a function). We will talk more about scope in a future article, but if you would like to learn more about it now, check out this [article on MDN](https://developer.mozilla.org/en-US/docs/Glossary/Scope).



```js
var yellowFruit = 'banana'; // outside of function -> global scope

function f() {
  var redFruit = 'strawberry'; // inside of function -> function scope
}

console.log(redFruit); // ReferenceError: redFruit is not defined, because redFruit is not in the global scope
```



In terms of hoisting, `var` variables are hoisted to the top of their scope and initialized with the value of `undefined`. We will talk more about hoisting in a future article, but if you would like to learn more about it now, check out this [article on MDN](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting).



```js
// What we write
console.log(favoriteSeason);
var favoriteSeason = 'spring';

// How it's interpreted
var favoriteSeason;
console.log(favoriteSeason);
favoriteSeason = 'spring';
```



## Let

`let` solves one of the major issues that come with `var`: `let` variables are not redeclarable *in the same scope* (more on this later). You don't have to worry about accidentally creating bugs in your code by redeclaring a variable that has already been declared. Doing this for example is not allowed:



```js
let name = 'Steve';
let name = 'Chris'; // SyntaxError: Identifier 'name' has already been declared
```



Just like `var`, `let` variables can also be reassigned.



```js
let age = 28;
age = 30;
```



In terms of scope, `let` variables are block scoped. A block is any code written between a pair of curly brackets `{ }`. Remember how `let` variables are not redeclarable *in the same scope* ? They are, however, redeclarable if they are in different scopes, as illustrated below.



```js
let yellowFruit = 'banana';

if (true) {
  let yellowFruit = 'lemon';
  console.log(yellowFruit); // lemon
}

console.log(yellowFruit); // banana
```



In terms of hoisting, `let` variables are hoisted to the top of their scope, but they are not initialized. This means that you cannot use `let` variables before declaring them.



```js
console.log(favoriteSeason);
let favoriteSeason = 'spring';  // ReferenceError: favoriteSeason is not defined
```



## Const

Just like `let`, `const` variables can also not be redeclared.



```js
const name = 'Steve';
const name = 'Chris';  // SyntaxError: Identifier 'name' has already been declared
```



Unlike both `var` and `let`, `const` variables can not be reassigned.



```js
const age = 28;
age = 30;  // TypeError: Assignment to constant variable.
```



When it comes to Objects declared with `const` - the Object itself cannot be reassigned, but the individual properties within the Object can be.



```js
const student = {
  name: 'Alice',
  age: 16
}

student.name = 'Kelly';  // works fine

student = {
  name: 'Susan',  // TypeError: Assignment to constant variable.
  age: 15
}
```



Just like `let`, `const` variables  are block scoped.



```js
const yellowFruit = 'banana';

if (true) {
  const yellowFruit = 'lemon';
  console.log(yellowFruit); // lemon
}

console.log(yellowFruit); // banana
```



Just like `let`, `const` variables  are hoisted to the top of their scope, but they are not initialized. 



```js
console.log(favoriteSeason);
const favoriteSeason = 'spring'; // ReferenceError: favoriteSeason is not defined
```



## When to Use Which?

For `let` and `const`, there are two main approaches regarding when to use which:

1. Use `let` by default, switch to `const` when you need a variable to remain constant.
2. Use `const` by default, switch to `let` when you need a variable to be reassignable.



What about `var`? The general consensus among JavaScript developers is that in modern JavaScript **YOU SHOULD NEVER USE VAR**, under any circumstances. `var` is simply worse compared to `let` and `const`, and there is no good reason to ever use it. Also, there's a chance your tech lead will hunt you down if they see `var` in your pull requests. 😄

---

## Practice

What are the outputs of these code snippets?

1. ```js
   if (true) {
     var year = 2022;
     let model = 'Golf';
   }
   
   console.log(year)
   console.log(model)
   ```

   **Answer:**

   ```
   2022
   ReferenceError: model is not defined
   ```

   **Reason:** `model` is declared using `let`, which means its scope is restricted to the code block of the `if` statement. Trying to access it outside of its scope will cause an error. `year` is declared using `var`, which is not block scoped and therefore can be accessed outside of the `if` statement.

   

2. ```js
   for (var i = 0; i < 3; i++) {
     console.log('Looping...')
   }
   
   console.log(i);
   ```

   **Answer:**

   ```
   Looping...
   Looping...
   Looping...
   3
   ```

   **Reason:** In this case `var` is declared globally, therefore `i` is accessible outside of the `for` loop.

   

3. ```js
   for (let i = 0; i < 3; i++) {
     console.log('Looping...')
   }
   
   console.log(i);
   ```

   **Answer:**

   ```
   Looping...
   Looping...
   Looping...
   Uncaught ReferenceError: i is not defined
   ```

   **Reason:** Because `let` is block scoped, `i` is restricted to the `for` loop and cannot be accessed outside of it.

---

Thank you for reading the second article in my Core JavaScript series! If you found this useful, if you have anything to add, or if I made any mistakes - I would love to hear from you! I'm also very open to suggestions for future topics for the series. 😊

Expect to see the next part soon. Thanks and see you there!