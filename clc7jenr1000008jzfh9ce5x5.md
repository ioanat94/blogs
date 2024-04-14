---
title: "Core JavaScript: Hoisting"
seoTitle: "Core JavaScript: Hoisting"
seoDescription: "This is an article in a series about core JavaScript principles. For beginners and more experienced developers in need of a refresher!"
datePublished: Wed Dec 28 2022 10:51:33 GMT+0000 (Coordinated Universal Time)
cuid: clc7jenr1000008jzfh9ce5x5
slug: core-javascript-hoisting
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1672224360504/07936c23-e72c-40ff-ab0d-d329b4e4b291.png
tags: hosting, javascript, beginners

---

## **About the series**

Core JavaScript is a series I'm writing that covers, as the name suggests, some of the core principles of JavaScript. It originally started as a study or reference material for myself, but I decided to share it with the community in the hopes that it will prove useful for others.

This series is intended for beginner JavaScript developers or more experienced developers in need of a refresher. I have a few topics planned out already, but I would love to hear from you if there are any topics, in particular, you would be interested to read about!

---

You might recall that in a [previous article](https://blog.ioanatiplea.dev/core-javascript-var-vs-let-vs-const) we came across the concept of hoisting in JavaScript. Essentially, hoisting is the process through which the declaration of a variable or function is moved to the top of its scope. It allows us to use variables and call functions before they appear in our code.

## **Declaration vs Assignment / Initialization**

It is important to note that only *declarations* are hoisted, and initializations and assignments are not. Below is the difference, in case you need a refresher.

```javascript
let number; // Declaration
number = 5; // Assignment
const name = 'John'; // Initialization
```

Consider the following examples:

```javascript
var first = 1;
var second = 2;
​
console.log(first + " " + second); // Output: 1 2
```

```javascript
var first = 1;
​
console.log(first + " " + second) // Output: 1 undefined
​
var second = 2;
```

Because declarations are hoisted to the top of the scope but initializations are not, the second example essentially gets translated to the following:

```javascript
var first = 1;
var second; // This is currently undefined
​
console.log(first + " " + second) // Output: 1 undefined
​
second = 2;
```

## **Var vs Let vs Const**

If you've read my previous article about variable types, you know that `var` variables are hoisted to the top of their scope and initialized with the value of `undefined`. Some consider `let` and `const` to be non-hoisted, which is not entirely correct. In reality, `let` and `const` variables are indeed hoisted to the top of their scope, but they are not initialized.

This means that with `var` we can do something like this:

```javascript
console.log(number); // undefined
var number = 5;
```

However, trying to do the same thing with `let` or `const` will throw an error:

```javascript
console.log(number); // ReferenceError: number is not defined
let number = 5;
```

## **Functions**

Hoisting works the same for functions as it does for variables - function declarations are hoisted, but function expressions are not.

```javascript
hoistedFunction(); 
      
function hoistedFunction() { // Function declaration
  console.log('This will work!');
}
​
// Output: This will work!
```

```javascript
nonHoistedFunction();
  
let nonHoistedFunction = () => { // Function expression
    console.log('This will not work...');
}
​
// Output: ReferenceError: nonHoistedFunction is not defined
```

If we use `var` instead of `let`, we still get an error, but of a different kind.

```javascript
nonHoistedFunction();
  
var nonHoistedFunction = () => { // Function expression
    console.log('This will still not work...');
}
​
// Output: TypeError: nonHoistedFunction is not a function
```

## **Tip - Declare variables at the top**

Hoisting is easy to forget about or overlook, which tends to lead to bugs and confusion. Declaring variables at the top of their scope helps you avoid errors and it keeps your code clean.

---

## **Practice**

What are the outputs of these code snippets?

1. ```javascript
    example();
    ​
    function example() {
      let name = 'Bon Jovi';
      console.log(name);
    }
    ```
    
    **Answer:**
    
    ```plaintext
    Bon Jovi
    ```
    
    **Reason:** `example()` is a function declaration, which is hoisted - therefore, it can be called before it appears in our code and everything will work as intended.
    
2. ```javascript
    example();
    
    ​function example() {
      console.log(name);
      let name = 'Bon Jovi';
    }
    ```
    
    **Answer:**
    
    ```plaintext
    ReferenceError: Cannot access 'name' before initialization
    ```
    
    **Reason:** `let` variables, despite being hoisted to the top of their scope, are not initialized. Therefore, we are warned that we cannot use `name` before it is initialized.
    
3. ```javascript
    example();
    ​
    let example = () => {
      let name;
      console.log(name);
      name = 'Bon Jovi';
    }
    ```
    
    **Answer:**
    
    ```plaintext
    ReferenceError: example is not defined
    ```
    
    **Reason:** Function expressions are not hoisted, therefore we cannot use them before they appear in the code. Because we are using `let` here, we get a ReferenceError.
    

---

Thank you for reading the third article in my Core JavaScript series! If you found this useful, if you have anything to add, or if I made any mistakes - I would love to hear from you! I'm also very open to suggestions for future topics for the series. 😊

Expect to see the next part soon. Thanks and see you there!