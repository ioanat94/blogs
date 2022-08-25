## Core JavaScript: Primitive vs. Non-primitive Data Types

## About the series

Core JavaScript is a series I'm writing that covers, as the name suggests, some of the core principles of JavaScript. It originally started as study or reference material for myself, but I decided to share it with the community in the hopes that it will prove useful for others. 

This series is intended for beginner JavaScript developers, or more experienced developers in need of a refresher. I have a few topics planned out already, but I would love to hear from you if there are any topics in particular you would be interested to read about!

---

In this article I will first go over the data types in JavaScript, after which I will talk about the differences between them, and I will end with a few exercises to practice the concepts I talked about.

## Data Types in JavaScript

Currently there are eight data types in JavaScript, which are divided into two categories: primitive and non-primitive.

<table border="0">
 <tr>
    <td style="text-align:center"><b>Primitive</b></td>
    <td style="text-align:center"><b>Non-primitive</b></td>
 </tr>
 <tr>
    <td>
        <ul style="text-align:center; list-style-type: none;">
            <li>Number</li>
            <li>BigInt</li>
            <li>String</li>
            <li>Boolean</li>
            <li>Null</li>
  			<li>Undefined</li>
            <li>Symbol</li>
        </ul>
     </td>
    <td style="vertical-align:top;">
        <ul style="text-align:center; list-style-type: none;">
            <li>Object</li>
        </ul>
    </td>
 </tr>
</table>

### Number

The `number` data type represents a positive or negative numeric value, which can be an integer or a float containing a decimal point or written using exponential notation. [Read more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#number_type)



```js
const integer = 2;
const float = 2.25;
const positiveExponent = 2.25e+7; // 22,500,000
const negativeExponent = 2.25e-7; // 0.000000225
```



### BigInt

`Number` is "limited" to storing numeric values between  -(2^53 − 1) and 2^53 − 1. If we need to use values that are outside of this range, we can use `BigInt`. They are declared by adding an "n" at the end of the numeric value. [Read more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#bigint_type)



```js
const reallyHighValue = 18014398509481982n;
const reallyLowValue = -18014398509481982n;
```



### String

`Strings` are used to store text. They are declared between quotation marks, which can be single quotes (' '), double quotes (" "), or backticks (\` \`). Single and double quotes are mostly interchangeable, whereas backticks allow you to insert variables into your `strings`. [Read more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#string_type)



```js
const singleQuotes = 'Hello';
const doubleQuotes = "World";

const name = 'John Doe';
const greeting = `Hello, ${name}!` // 'Hello, John Doe!'
```



### Boolean

`Booleans` allow you to add logic to your application. Their value can be either `true` or `false`. [Read more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#boolean_type)



```js
const isOpen = true;
const hasValue = false;
```



### Null

`Null` expresses a lack of value. In other words, if a variable that is `null`, we know that it exists, but it is an empty variable. [Read more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#null_type)



```js
const value = null;
```



### Undefined

`Undefined` represents a variable that has been declared but not assigned a value. [Read more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#undefined_type)



```js
const value;
console.log(value); // undefined
```



### Symbol

A `symbol` is a unique and immutable value. It can be used as the key of an `Object` property. [Read more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#symbol_type)



```js
const mySymbol = Symbol('Some Value');

const name = Symbol();
const age = Symbol();
const student = {
  [name]: 'Mark Twain',
  [age]: 21
}
```



### Object

`Objects` allow us to store more complex data in the form of key-value pairs called properties. If a property of an `Object` is a function, it is called a method. `Arrays` and `functions` are also `Objects` in JavaScript. [Read more.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#objects)



```js
const apple = {
  count: 5,
  color: ['red', 'green'],
  taste: 'sweet',
  fresh: true,
  describe : function() {
  return 'I\'ve got ' + this.count + ' ' + this.taste + ' apples.'; // I've got 5 sweet apples.
  }
}
```
---
## Differences Between Primitive and Non-Primitive Data Types

There are three main differences between primitive and non-primitive data types, and they are all rather closely related.

### Stored as Value vs. Stored as Reference

The core difference between primitive and non-primitive data types in JavaScript is the way they are stored in memory: primitives are stored as a *value* in memory, whereas non-primitives are stored as a *reference to an address* in memory. This will become relevant shortly.



```js
const a = 'John';       // a refers to a *value* in memory.
const b = {             // b refers to an *address* in memory.
  firstName: 'John',
  lastName: 'Doe'
}
```



### Compared by Value vs. Compared by Reference

Much like the way they are stored in memory, primitives are compared by *value*, whereas non-primitives are compared by *reference*. To understand the difference, consider these examples:



```js
let a = 1;
let b = a; 
a === b;  // true

let a = 1;
let b = 1;
a === b;  // true
```



At first glance, this behavior seems obvious. But compare it to the behavior of non-primitives:



```js
// Case 1
let a = { x: 1, y: 2 };
let b = a;
a === b;  // true

// Case 2
let a = { x: 1, y: 2 };
let b = { x: 1, y: 2 };
a === b;  // false
```



In the first case, `a` and `b` share the same values *and* they point to location in memory, therefore `===` will return `true`. In the second example, `===` returns `false` because even though `a` and `b` have the same values, they point to different locations in memory.



### Mutable vs. Immutable

Primitive values are immutable. They can be reassigned to a new value, but you can't modify an already existing value. For example, you can't directly change a letter of a string.



```js
let string = 'Modify me!';
string = 'Modified string.'; // works fine
string[0] = 'Z';  // does nothing
```



Non-primitive values are mutable - we can modify already existing values as we please.



```js
let students = ['Alex', 'Stacy', 'Angela'];
students[0] = 'John';  // works fine
```
---
## Practice

What are the outputs of these code snippets?


1. ```js
    let a = 1;
    let b = 2;
    b = 3;
   
   console.log(a);
   console.log(b);
   ```

    **Answer:**

    ```js
    1
    3
    ```

    **Reason:** Primitive values are independent - `a` and `b` are stored in different locations in memory. Therefore, modifying one does not affect the other.
2. ```js
    let a = 'Who you gonna call?';
    let b = a;
    b = 'Ghostbusters!';
    
    console.log(a);
    console.log(b);
    ```
    
    **Answer:**
    
    ```js
    Who you gonna call?
    Ghostbusters!
    ```

    **Reason:** Same as exercise 1.  
3. ```js
    let a = { favoriteColor: 'red' };
    let b = a;
    a.favoriteColor = 'green';
    
    console.log(b.favoriteColor);
    ```
    
    **Answer:**
    
    ```js
    green
    ```
    
    **Reason:** Non-primitive values are stored as references to addresses in memory. Therefore, `a` and `b` share the same address, which means that changing one will also affect the other.
---
Thank you for reading the very first article in my Core JavaScript series! If you found this useful, if you have anything to add, or if I made any mistakes - I would love to hear from you! I'm also very open to suggestions for future topics for the series. 😊

Expect to see the second part soon. Thanks and see you there!