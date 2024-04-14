---
title: "Core JavaScript: Scope"
seoTitle: "Core JavaScript: Scope"
seoDescription: "This is an article in a series about core JavaScript principles. For beginners and more experienced developers in need of a refresher!"
datePublished: Thu Jan 12 2023 08:00:08 GMT+0000 (Coordinated Universal Time)
cuid: clcssvz8e000c08mqcru200lz
slug: core-javascript-scope
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1673508649345/5029ed75-943f-411a-b706-af495295d651.png
tags: javascript, beginners, scope

---

## **About the series**

Core JavaScript is a series I'm writing that covers, as the name suggests, some of the core principles of JavaScript. It originally started as a study or reference material for myself, but I decided to share it with the community in the hopes that it will prove useful for others.

This series is intended for beginner JavaScript developers or more experienced developers in need of a refresher. I have a few topics planned out already, but I would love to hear from you if there are any topics, in particular, you would be interested to read about!

---

You might recall that in a [previous article](https://blog.ioanatiplea.dev/core-javascript-var-vs-let-vs-const), we came across the concept of scope in JavaScript. In short, scope represents the section of code in which a variable is accessible. There are a few different types of scope in JavaScript:

* Global scope
    
* Module scope
    
* Function scope
    
* Block scope
    

Let's go through each of them to see how they work.

## **Global scope**

The global scope exists outside of any functions. Variables declared in the global scope are called *global variables*, and they can be accessed anywhere in the code.

```javascript
const name = 'Jane'; // Global variable, in global scope
​
function greet() {
    console.log(`Hello, ${name}!`); // Hello, Jane!
}
```

**Note:** If you assign a value to a variable that has not yet been declared, it automatically becomes a global variable, unless you are using [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode).

```javascript
function greet() {
    name = 'Jane';
    console.log(`Hello, ${name}!`); // Hello, Jane!
}
```

## **Module scope**

With the introduction of modules in ES2015 also came the concept of module scope. Consider the following module, `greeting`:

```javascript
// greeting.js
​
const name = 'John';
​
console.log(`Hello, ${name}!`);
```

Let's import the module into a different file and try to access `name`:

```javascript
import '../greeting.js'
​
console.log(name);
```

This will throw an error, because `name` is not accessible outside its module, `greeting`, unless it is exported.

## **Function scope**

In JavaScript, each function creates its own scope. Variables declared within a function scope are called *local variables*, and they can only be accessed within the function they have been declared in.

```javascript
function greet() {
    const name = 'John'; // Local variable, in function scope
    
    console.log(`Hello, ${name}!`);
}
​
greet(); // Hello, John!
console.log(name); // ReferenceError: name is not defined
```

## **Block scope**

Block scope is the scope that exists within a pair of curly brackets `{ }`. Variables declared within a block scope are only accessible within that scope.

```javascript
if (true) {
    const name = 'John'; // Block-scoped variable
    
    console.log(`Hello, ${name}!`); // Hello, John!
}
​
console.log(name); // ReferenceError: name is not defined
```

**Note:** `var` variables behave differently in this scenario - they are not block scoped! `var` variables can be accessed outside of the block scope (but not outside of the function scope!).

```javascript
if (true) {
    var name = 'John'; // Block-scoped variable
    
    console.log(`Hello, ${name}!`); // Hello, John!
}
​
console.log(name); // John
```

## **Scope nesting**

In JavaScript, scopes can be nested, meaning that a scope can exist inside another scope.

```javascript
function greet() {
    // Function scope of the greet function
    const name = 'John';
    
    if (name === 'John') {
        // Block scope of the if-statement
        const greeting = 'Hello';
        console.log(`${greeting}, ${name}!`); // Hello, John!
    }
    
    console.log(greeting); // ReferenceError: greeting is not defined
}
```

The scope of the `greet` function is called the *outer scope*, and the scope of the `if` statement is called the *inner scope*. The important takeaway here is that variables declared in the outer scope can be accessed in the inner scope, but variables declared in the inner scope cannot be accessed in the outer scope.

## **Scope chain**

Whenever you try to access a variable within your code, the search process begins from the local scope of the function you are calling. If the variable does not exist in the local scope, the search moves on to the outer scope (e.g. the scope of a parent function) until it reaches the outermost scope of the code - the global scope. This path that the code goes down in order to find the variable is known as the *scope chain*. If the variable is not found anywhere along the way, you will get a ReferenceError.

---

## **Practice**

What are the outputs of these code snippets?

1. ```javascript
    function greet() {
        let name = 'John';
        console.log(`Hello, ${name}!`)
    }
    ​
    name = 'Jane';
    greet();
    console.log(`Hello, ${name}!`);
    ```
    
    **Answer:**
    
    ```javascript
    Hello, John!
    Hello, Jane!
    ```
    
    **Reason:** The `name` inside of the `greet` function is a local variable, so it cannot be changed from outside of the function. `name = 'Jane';` essentially creates a new global variable.
    
2. ```javascript
    let name = 'John';
    ​
    if (true) {
      let name = 'Jane';
    }
    ​
    console.log(name);
    ```
    
    **Answer:**
    
    ```javascript
    John
    ```
    
    **Reason:** The `name` variable with the value `Jane` is created within the block scope of the `if` statement. Therefore, it cannot be accessed from the global scope. Instead, `name` will have the value given to it in the global scope, which is `John`.
    
3. ```javascript
    let name = 'John';
    ​
    if (true) {
      var name = 'Jane';
    }
    ​
    console.log(name);
    ```
    
    **Answer:**
    
    ```javascript
    SyntaxError: Identifier 'name' has already been declared
    ```
    
    **Reason:** `var` does not follow the same rules as `let` and `const` - its declaration will be global despite being placed inside of the `if` block. Therefore, the code will throw an error as `name` has already been declared in the global scope.
    

---

Thank you for reading this article in my Core JavaScript series! If you found this useful, if you have anything to add, or if I made any mistakes - I would love to hear from you! I'm also very open to suggestions for future topics for the series. 😊

Expect to see the next part soon. Thanks and see you there!