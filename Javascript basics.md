# Javascript Basics

## How to run javascript code?
- Just like any other language, source code needs to be converted into machine language. There are 2 methods to do that:
    1. Classic way (in the browser)
        - `index.html` with a `<script>` tag which includes a `src` attribute which contains the path to the `script.js` file
        - `script.js` which contains the code
        - In this method we run a `html` file in the browser, and the browser's js engine runs the `js` file
    2. Js Engine
        - This method allows us to run javascript code outside of the browser
        - E.g.: V8 (by google), Spider Monkey (by mozilla), node

## History of javascript
- It was one of many scripting languages
- It's primary function was to enable developers to make dynamic web pages, but now it can do much more
- It adheres to the ECMAscript standard, which is a guideline for scripting languages

## Variables
- `var`, `const` or `let` keywords can be used for declaring variables
```js
var variable1 = value;
var variable2;
variable2 = value;
```
- `const` is used to make a variable constant, we can not change the value of a constant variable
```js
const accNo = 35;
accNo = 48; // TypeError: Assignment to constant variable
```
- `let` is used to constrain the scope of a variable to the scope in which it is declared, it is frequently used for counter variables in loops
```js
{
    var birthYear = 2001;
    var currYear = 2021;
    let age = currYear - birthYear;
    console.log(age); // 20
}
console.log(birthYear, currYear); // 2001 2021
console.log(age); // ReferenceError: age is not defined
```

### Variable naming conventions
- Usually start with lowercase letters
- Cannot start with a number
- Should not start with an underscore, it is used for other things

## Comments
- Single-line comment
```js
// This is a comment
```
- Multi-line comment
```js
/* This is a
Multi-line comment */
```

## Datatypes
1. Strings
- They are enclosed in either single-quotes (`''`) or double-quotes (`""`)
- String literals can be written using back-ticks (``` `` ```)
```js
var firstName = 'Idu';
var lastName = "Who";
var story = `drink
some
water`;
```
2. Boolean
```js
var isHydrated = true;
var isAlive = false;
```
3. Number
```js
var rollNo = 69;
```
4. `undefined`
- When a value has not been assigned to a variable, it contains `undefined`
```js
var marks;
console.log(marks); // undefined
```

## Printing to Console
- `console.log()` is used to print a string onto the console
- To print multiple items, we can use one of the following methods:
    1. Concatenate all items into a single string using `+`
    ```js
    console.log("Roll No: " + rollNo + "\nName: " + firstName + "\nMarks: " + marks);
    ```
    2. Write the items as separate arguments, this also adds a space between the items
    ```js
    console.log("Roll No:",rollNo,"\nName:",firstName,"\nMarks:",marks);
    ```
    3. Use a string literal and `${}`, which is know as _interpolation_
    ```js
    console.log(`Roll No: ${rollNo}
    Name: ${firstName}
    Marks: ${marks}`);
    ```

## Operators

### Arithmetic operators
1. Addition (`+`)
2. Subtraction (`-`)
3. Division (`/`)
4. Multiplication (`*`)
5. Modulus (`%`)
6. Exponential (`**`)

### Relational operators
1. Equality (`==`)
2. Inequality (`!=`)
3. Strict equality/Identity (`===`)
4. Strict inequality/Non-identity (`!==`)
5. Greater than (`>`)
6. Less than (`<`)
7. Greater than or equal to (`>=`)
9. Less than or equal to (`<=`)

### Logical operators
1. AND (`&&`)
2. OR (`||`)
3. NOT (`!`)

### `typeof` operator
- returns a string containing the datatype of a value, variable or expression
```js
console.log(typeof 20); // number
console.log(typeof "hi"); // string
console.log(typeof true); // boolean
console.log(typeof undefinedVariable); // undefined
console.log(typeof NaN); // number
console.log(typeof null); //object
```

> **NOTE:** `typeof null` returns `object` as all objects are derived from `null`

### Conditional (ternary) operator
- It is frequently used as a shourcut to the `if` statement.
```js
condition? trueExpression : falseExpression;
```

## Precedence of Operators
*[Read this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)*

## Contol Flow Statements
- They are used to control the flow of the program

### `if... else` statement
```js
if (condition) {
    // true statements
} else {
    // false statements
}
```

### `switch` case
```js
switch (expression) {
    case expression:
        // true statements1
        break;
    case expression:
        // true statement2
        break;
    default:
        // default statement
}
```

## Looping Statements
- They are used to loop a block of statements based on a condition

### `for` loop
```js
for (declaration; condition; increment/decrement counter) {
    // looping statements
}
```

### `while` loop
```js
let counter = initial_value;
while (condition) {
    // looping statements
    // increment/decrement counter
}
```

### `do... while` loop
```js
let counter = initial_value;
do {
    // looping statements
    // increment/decrement counter
} while (condition);
```

### `for of` loop
- It is used to loop through elements of an arrays
```js
var myArray = [1, 2, 3];
for (var element_valriable of myArray) {
    // looping statements
}
```

### `for in` loop
- It is used to loop through members of an object
```js
var myObject = {
    myMember1 = 1,
    myMember2 = 2,
    myMember3 = 3,
}
for (var member in myObject) {
    // looping statements
}
```

## Type Coercion
- It is the process of implicitly/automatically converting from one datatype to another

### Truthy and Falsy values
- While using conditional expressions it should be kept in mind that non-boolean values are coerced to boolean values in a boolean context
- _falsy_ values are values that get coerced to `false`. A few examples of falsy values are `0`, `-0`, empty string value (`""`, `''`, or ``` `` ```), `null`, `undefined`, `NaN`
- _truthy_ values are values which are not _falsy_

> **NOTE:** when the 1st operand in a Logical AND (`&&`) operation is falsy, the result is the falsy value

### Coercion to String
- When a string and a non-string value are concatenated/added the non-string value is coerced into a string, and then both values are concatenated
```js
console.log("go"+2); // go2
console.log(6 + '8'); // 68
console.log(true + "fru"); // truefru
console.log("something" + null); // somethingnull
console.log(undefinedVariable + ":("); // undefined:(
console.log(NaN + `MaN`); // NaNMaN
```

> **NOTE:** `true`, `false`, `null`, `undefined`, `NaN` coerced into strings are just strings containing the name of the value


### Coercion to Number
- When a subtraction (`-`), multiplication (`*`), division (`/`) or modulus (`%`) operation is performed, all non-number operands are coerced into numbers; as these operations can only be performed on numbers
```js
console.log("100"-31); // 69
console.log('     8.99' - `0.00000001  `); //8.98999999
console.log('2' * "abc"); // NaN
console.log("10" / "5"); // 2
console.log("10" % "5"); // 0
console.log(99 * null); // 0
console.log(100 - true); // 99
console.log(false * 8); // 0
```

> **NOTE:** `null` coerced into a number is 0, `undefined` coerced into a number is `NaN`

> **NOTE:** `true` and `false` coerced into numbers are 1 and 0 respectively

> **NOTE:** boolean and falsy values can also be added with numbers. But strings can not implicitly be added with numbers because when performing addition the number is coerced into a string.

### Equality operator
- When datatypes of the operands are not the same, the non-number operands are coerced into numbers and then compared
```js
console.log(1 == '1'); // true
console.log(0 == false); // true
console.log('true' == true); // false
console.log(true == '1'); // true
```

| **Operator** | **Coerced Datatype** | **Initial Datatypes** |
| :----: | :---- | :---- |
| `+` | string | number, boolean, `null`, `undefined`, `NaN` |
| `+` | number (when there is no string operand) | boolean, `null`, `undefined` |
| `-`, `*`, `/`, `%` | number | string, boolean, `null`, `undefined` |
| `==` | number (when datatypes of operands don't match) | string, boolean |

## Functions
- It is a named block of code, which can be reused
```js
function functionName() {
    // statements
}
```
- We can run a function by calling it
```js
functionName();
```
- We can reference a function by  name without parenthesis
```js
functionName;
```
- To make functions dynamic we can pass arguments to it
```js
function functionName(argument1, argument2, ..., argumentn) {
    // statements
}
functionName(value1, value2, ..., valuen);
```
- The `return` keyword can be used to return a value from the function
```js
function functionName() {
    // statements
    return value;
}
console.log(functionName()); // value
```
- We can also store functions in variables
```js
var variableName = function (argument1, argument2, ..., argumentn) {
    // statements
    return value;
}
```
- Functions are available globally, but when a function is stored in a variable it is not available globally

## Context
- The context is the environment in which everything resides
- Examples of different contexts:
    1. When the code executes in the browser the context is `window`
    2. When the code executes on a js engine outside the browser the context is different
- All function definitions in a particular context are scanned and stored in the context. This makes them available to use anywhere in that context
- All variable declarations are scanned and set as undefined
```js
// calling a function before its definition
console.log(greet("Norm")); // Hi Norm!
function greet(name) {
    return `Hi ${name}!`;
}
// using a variable before its definition
console.log(marks); // undefined
var marks = 77;
// using a variable containing a function before its definition
console.log(tot(1, 2, 3)); // TypeError: tot is not a function
var tot = function (mrks1,mrks2,mrks3) {
    return mrks1 + mrks2 + mrks3;
}
// trying to use a function outside the context it is defined in
function outerFunc() {
    console.log("outer");
    innerFunc();
    function innerFunc() {
        console.log("inner");
    }
}
outerFunc();
innerFunc(); // ReferenceError: innerFunc is not defined
```

### Types of contexts
1. Global context
    - It is responsible for collecting information
2. Execution context
    - It is responsible for executing code
    - For single-line of code like `console.log()`, an execution context is created and then destroyed once the code has completed execution
    - For a function, a larger execution context is created, all the code within the function is executed inside the functions execution context, the execution context is destroyed once the function completes its execution

### Scope chaining
- Technically a scope is defined by curly braces (`{}`) but only functions behave as scopes in scope chaining
- Scope chaining is a feature of execution contexts which enables inner/smaller scopes to access information that exists in outer/larger scopes when the information is not present in the smaller scope
- The scope of a function is based on where the function is defined, and the information that a function can access is also based on where it is defined.
```js
// example of scope chaining
var x = 1;
function scopeChainingFunc() {
    console.log(x); // 1
}
scopeChainingFunc();
// example of scope chaining where the variable is defined after the function call
function scopeChainingFunc2() {
    console.log(y); // undefined
}
scopeChainingFunc2();
var y = 2;
// example of non-scope chaining function, where the variable exists in the function's scope
function nonScopeChainingFunc() {
    var x = 3;
    console.log(x); // 3
}
nonScopeChainingFunc();
// nested functions
function outerFunc() {
    console.log(x); // undefined
    function innerFunc() {
        console.log(x); // 4
    }
    var x = 4;
    innerFunc();
}
outerFunc();
```

## Arrays
- It is an ordered collection of related values, it is not homogeneous
- It is a mutable data structure
- There are 2 methods of defining an array
```js
var arrayName = ["value1", "value2", ..., "valuen"];
var arrayName1 = new Array("value1", "value2", "value3");
```
- We can access an element from an array by specifying it's index
```js
console.log(arrayName1[0]); // 'value1'
```
- Reassigning an element in the array
```js
arrayName1[0] = 1;
console.log(arrayName1); // [1, 'value2', 'value3']
```

### Array methods and attributes
1. `length`
    - Stores the number of elements present in the array
    ```js
    var myArr = [1, 2, 3, 4, 5];
    console.log(myArr.length); // 5
    ```
2. `pop()`
    - Returns and removes the last element from the array
    ```js
    console.log(myArr); // [1, 2, 3, 4, 5]
    console.log(myArr.pop()); // 5
    console.log(myArr); // [1, 2, 3, 4]
    ```
3. `push()`
    - Adds an element to the end of the array, and returns the updated length of the array
    ```js
    console.log(myArr); // [1, 2, 3, 4]
    console.log(myArr.push(5)); // 5
    console.log(myArr); // [1, 2, 3, 4, 5]
    ```
4. `unshift()`
    - Shifts all elements to the right and adds the element passed to it as an argument as a new element at the 0th index, and returns the length of the array
    ```js
    console.log(myArr); // [1, 2, 3, 4, 5]
    myArr.unshift(0);
    console.log(myArr); // [0, 1, 2, 3, 4, 5]
    ```
5. `shift()`
    - Shifts all elements to the left, and removes and returns the element at the 0th index
    ```js
    console.log(myArr); // [0, 1, 2, 3, 4, 5]
    console.log(myArr.shift()); // 0
    console.log(myArr); // [1, 2, 3, 4, 5]
    ```
6. `indexOf()`
    - Takes a value as an argument, searches for it in the array and returns the index of the element if it matches the given value, if the value does not exist in the array it returns -1
    ```js
    console.log(myArr); // [1, 2, 3, 4, 5]
    console.log(myArr.indexOf(1)); // 0
    console.log(myArr.indexOf(9)); // -1
    ```
7. `slice()`
    - Returns a slice of the array, starting from the given beginning index (include) and ending before the ending index (excluded)
    - default value of the ending index is the length of the array
    ```js
    console.log(myArr); // [1, 2, 3, 4, 5]
    console.log(myArr.slice(1,4)); // [2, 3, 4]
    console.log(myArr.slice(2)); // [3, 4, 5]
    ```
8. `splice()`
    - Returns and removes a part of the array, and replaces it with the provided values
    - The part to remove is specified by a starting index, and the count which denotes the number of elements to remove
    ```js
    console.log(myArr); // [1, 2, 3, 4, 5]
    console.log(myArr.splice(1, 2, "2", "3")); // [2, 3]
    console.log(myArr); // [1, '2', '3', 4, 5]
    ```
9. `fill()`
    - Replaces a slice of the array with a value, and returns the result, if the ending index is not provided the length of the array is taken
    ```js
    console.log(myArr); // [1, '2', '3', 4, 5]
    console.log(myArr.fill(null,1,3)); // [1, null, null, 4, 5]
    ```
10. `filter()`
    - Takes a call back function as an argument and returns an array of elements for which the function returns truthy
    ```js
    console.log(myArr); // [1, null, null, 4, 5]
    console.log(myArr.filter((e) => typeof e == 'number')); // [1, 8, 8, 8]
    ```
11. `every()`
    - Takes a call back function as an argument and returns true if the function returns true for every value of the array else it returns false
    ```js
    console.log(myArr); // [1, null, null, 4, 5]
    console.log(myArr.every((e) => e >= 0)); // true
    ```
12. `forEach()`
    - Takes a call back function as an argument to which we can pass elements of the array, the call back function will be run for all elements of the array
    ```js
    console.log(myArr); // [1, null, null, 4, 5]
    myArr.forEach((element) => console.log(typeof element))
    // number
    // object
    // object
    // number
    // number
    ```

### Static methods of array
1. `Array.from()`
    - Creates an array from any iterable (like a string)
    ```js
    console.log(Array.from('hello')); // [ 'h', 'e', 'l', 'l', 'o' ]
    ```

## Objects
- It is used to store `key:value` pairs, and other complex entities
```js
// normal syntax
var objectName1 = {member1: "value1", member2: "value2"};
// commonly used syntax for increased readability
var objectName2 = {
    member1: "value1",
    member2: "value2",
}
```
- Members of an object are separated by comma (`,`)
- Data members/attributes of an object are created by writing their name as a key and the value after a semi-colon (`:`)
- Member names can also be written as a string
```js
var myObj1 = {
    'member1': 1,
    "member2": true,
}
```
- Member functions/methods can be defined by writing the name as a key and an anonymous function as the value
- The `this` keyword can be used to refer to the object from inside a member function
```js
var myObj2 = {
    sum: 0,
    add: function (num1, num2) {
        this.sum = num1 + num2;
    },
}
```
- Members of an object can be accessed either by using the _dot operator_ (`.`) or by writing the member name in a string inside square brackets (`[]`)
```js
console.log(ObjectName1.member1); // 'value 1'
console.log(ObjectName1["member2"]); // 'value 2'
```
- The entire object can be displayed as well by using `console.log()` or `console.table()`
```js
console.log(myObj1); // { member1: 1, member2: true }
console.table(myObj1);
// +---------+--------+
// | (index) | Values |
// +---------+--------+
// | member1 |   1    |
// | member2 |  true  |
// +---------+--------+
```

## `this` keyword
- It is used to refer to the object of the current context
- In the case of regular functions (non-member functions) `this` points to the object of the global context (`window` object in browsers)
- Whereas in the case of methods (member functions) `this` points to the object to which the member function belongs

## What is DOM?
- It is a way to represent the hierarchical structure of a html document
- In javascript the DOM is represented as the `document` object

### Selecting an element from DOM
1. `getElementById()`
    - The `getElementById()` method of the `document` object returns an object of the element that matches the id
    - It takes a string containing the id as an argument
    ```js
    document.getElementById("id_to_search");
    ```
2. `getElementsByXXX()`
    - The `getElementsByXXX` methods of the `document` object returns an array of objects which match the given condition
    - Elements can be filtered on the basis of `ClassName`, `Name`, `TagName` and `TagNameNS`
    - It takes a string containing the value to filter on as an argument
    ```js
    document.getElementsByClassName("className_to_search");
    document.getElementsByName("element_to_search");
    document.getElementsByTagName("tagName_to_search");
    document.getElementsByTagNameNS("tagName_to_search");
    ```
3. `querySelector()`
    - The `querySelector()` method of the `document` object returns the **first occurrence** of an element which matches the given conditions
    - Conditions to filter elements are written in a string and passed to the method
        - to select a particular html tag the tags name can be written
        - to select an element of a particular class the class name can be written preceded by a dot (`.`)
        - to select an element with a particular id the element's id can be written preceded by a hash (`#`)
    - When multiple values are passed for finding, it finds the element which satisfy all conditions
    ```js
    document.querySelector("h1"); // returns an object of a h1 tag
    document.querySelector(".title"); // returns an object of an element of the title class
    document.querySelector("#submit-button"); // returns an object of an element with the submit-button id
    ```
4. `querySelectorAll()`
    - It is the same as `querySelector()` but returns an array of objects of **all** elements which matched the conditions

<!--interpolation and injection, hoisting?-->
<!-- arrow function - are function stores in a variable they are written by specifying the arguments in parenthesis and then an arrow => and then a block of code, it is necessary to write a return keyword in arrow functions
call back function - they don't have a name, they can be written using arrow functions, when you have no return keyword and only a single line of code you don't write it as a block you just write the line as is-->
<!--to get the css properties of a class we can use window.getComputedStyle(objOfElement) which returns an object containing the properties of the element in a javascript syntax, the computed property removes the dashes from the property names and uses Camel case, to access a particular property about the element we can do it the same way we access a member of an object-->
<!-- time events in javascript: 1. setTimeout(function, milliseconds) - once the specified amount of time has passed the function will be executed, 2. setInterval(function, milliseconds) - it specifies an amount of time during which the function should be executed-->
<!--Events - when a button is clicked, when something is typed in a text input. There are different types of events like, resource events, network events, focus events, mouse events, etc. we can use .addEventListner('eventname', callback function) to add an event listener which reacts when the specified event is performed on a particular element-->
<!--elementObject.style() is used to apply a style, it can be used to get a style but usually getComputedStyle() is used for that-->
<!--Creating objects using a functional approach
when `new` is used on a function it treats it like a constructor and returns an object of the function, if the this keyword is used within that function it refers to the object of the function, but if the function refers to members with the this keyword and they don't exist then they are created within the object, the object can be stored in a variable
if the function is run without a new keyword but has a this key word, it will refer to the object of the global context, if a member which does not exist is referred to with the this keyword it will be created in the global context-->
<!--prototype - it allows you to add a attribute/method to an existing object without changing its definition, all objects have a __proto__, Syntax: object.prototype.new_member_to_add = value/function, DOUBT: does this add a member to the original object or only to objects created from the original object using the new keyword
__proto__ actually contains all the predefined code that is put there by JavaScript, and you can can add things to the proto of an object ot make them available for all instances of that object-->
<!--prototype chaining - object.hasOwnProperty("propertyName") takes a property and checks if it is present in the object-->
<!--Object.assign(targetObject, sourceObject) - assigns the values of the properties of the sourceObject to the target Object if those properties are found in the targetObject, and it returns the targetObject with the new values
Object.create(existingObject) - takes an existingObject and creates a new object from it, it returns the new object. but the properties and methods of the existing object are stored in the __proto__ of the new object, this method also allows us to initialize the attributes of the like how we can with constructors but it has a different syntax:
Object.create(existingObject, {
    attribute1: {value: "value1"},
    attribute2: {value: 3},
    newAttrubuteToAdd: {value: "newAttrubute"},
})-->
<!--in functional programming functions are treated as first class citizens or like variable - they can be stored in a variable, they can be passed as an argument to other functions : self executing anonymous function or IIFE (immediately invoked function expression)-->
<!--lexical scoping - (functional programming is the new way of writing JavaScript but its not the original way) the scope of a variable is limited to the scope function it is defined in, inner functions can use it be not outer functions.
but what is the function returns a reference to another function defined inside of it, then even when the function completes its execution its execution context can't be removed from memory as it contains the definition to which the reference points
closure (used by redux library) - it allows a function to returns a reference to a function defined in its scope
curring - when a function returns a reference to another function and that function is called directly by another pair of parenthesis. Syntax: function(parameters)(parameters)-->
<!--an object's method has its own __proto__ and if we have another object with similar attributes we can apply the method to another object by using the bind() method of the member function, bind() returns a reference of a function which is the same as the method it is binding but it changes the object that the this keyword points to from the object that the member function is defined in to the object that is passed to the bind() method as an argument-->

<!--make a simple crud application which allows the user to create, read, update and delete data from a database-->
<!--make a follower counter that ticks up to the follower amount-->
<!--make a simple online launchpad website which works with touch screens, and has a color changing music visualizer which changes colors based on the button being pressed-->
<!-- things to learn in JavaScript:
1. Equality: == and ===, == converts datatypes and then compares, === does not convert datatypes, for primitives the values of the primitives are compared but for objects the the values are not compared but whether or not the objects point to the same objects in memory
2. Async JS: call back functions - is the function which runs after another function runs, but that got complicated with call backs inside of other call backs - call back hell, so .then and .catch were added, .then handles what to do after successful execution of a function and .catch handles what to do after an error occurs in a function, then async await was added which makes the program wait for a response, also what is a promise
3. Error handling: checking how things can go wrong maybe the types of a parameter is incorrect maybe it is null or undefined, using try... catch to handle code that can throw errors
4. ES6 Syntax: differentiates between old and new JavaScript,
key features:
  * destructing
  * spread operator
  * literal strings which allow interpolation
5. array methods: map, filter, reduce, sum, every, sort. their syntax is tricky when combined with arrow function and abbreviated arrow function syntax-->
<!--beginner project:
1. password validator or password generator
2. tic tac toe game
3. basic website
algorithm visualizer
soduko solver
schedule manager
make an api
a group chat website using websocket
learn how to send push, sms, and email notifications. learn how to make a whatsapp chat bot, learn how to check the system theme and make the web page automatically adapt to light/dark mode depending on it-->
