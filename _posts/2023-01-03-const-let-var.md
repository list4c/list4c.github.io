---
layout: post
title:  "What's the difference between const, let and var in JavaScript?"
date:   2023-01-03 22:08:00 +0100
---

This article was inspired by a technical interview I've had recently
to verify my skills as a test automation engineer. My answer was
somewhat vague, but passable. If you're applying for any position 
where you're going to use JavaScript on a daily basis, there's a
decent probability you'll get asked this one. So let's explore the
differences in detail.

# var

`var` is an older way (before ES6 standard) to declare variables and is no
longer recommended as there as some pitfalls that make debugging harder. 

Examples of `var` usage:

```javascript

// Simple cases
var x = 10
console.log(x) // 10

var greeting = "Hello"
console.log(greeting) // "Hello"

// Re-assignment of value
var greeting = "Hello"
console.log(greeting) // "Hello"
greeting = "🙇"  // bowing gesture
console.log(greeting) //  🙇


// Declaration without value 
var later // declaration of the variable, without initialisation
console.log(later) // undefined
later = 100
console.log(later) // 100



// Declaration without the var keyword. Equivalent to previous example
weather = "Sunny" // also possible with var
console.log(weather) // "Sunny"



// Re-declaration of same variable

var lifeIsHard = true 
console.log(lifeIsHard); // true

if (lifeIsHard === true) {
  var lifeIsHard = false;      // no error, variable was re-declared

  console.log(lifeIsHard);  // false
}

console.log(lifeIsHard); // false. The re-declaration of variable took place globally



// var is available within function scope   

function makeMoo() {
    var cow = "Moo";
    console.log(cow); // Moo

    {
        var cat = "Meow";
        console.log(cat); // Meow
        console.log(cow); // Moo
    }
    console.log(cat) // would be an error if let was used 
}
makeMoo();


// Hoisting - a variable can be used before declaration

function hoisting() {
    console.log(hoistedVariable); // undefined
    var hoistedVariable = "hoisted";
}

hoisting(); // undefined - instead of error 



```

The main problems concerning var:
* it has function scope instead of block scope - see example in [MDN docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
* hoisting - see example above
* var creates a property on the global object
* re-declaration of the same variable


#### let

`let` is the new standard to declare variables. One can re-assign the value of a variable declared with `let` multiple times. 

```javascript

// Declaration with initialisation
let fruit = ['apple', 'banana', 'orange'];
console.log(fruit) // ['apple', 'banana', 'orange']

// Re-assignment of value
fruit = "no fruit in the basket";
console.log(fruit) // "no fruit in the basket"

// Declaration without value
let vegetables;
console.log(vegetables) // undefined

// Re-declaration of same variable (not possible in strict mode)
'use strict';
let lifeIsHard = true
console.log(lifeIsHard); // true
let lifeIsHard = false // error: Identifier 'lifeIsHard' has already been declared

// Initialisation of let variable without declaration
console.log(people) // Uncaught ReferenceError: people is not defined
let people = ['George', 'John', 'Paul', 'Ringo']
```

### const

```javascript

// Declaration of constant
const EARTH_RADIUS = 6371 // note: it's a convention to use uppercase for constants
EARTH_RADIUS = 9000 // error: Assignment to constant variable

// Re-declaration of same constant
const DEFAULT_COUNTRY='Poland'
const DEFAULT_COUNTRY='Germany' // error: Identifier 'defaultCountry' has already been declared
    
// Re-assignment of value
const DEFAULT_FRUIT='Banana'
DEFAULT_FRUIT='Apple' // error: Assignment to constant variable


```
Key points:

* `const` is the standard way to declare constants. 
* One can NOT re-assign values once assigned to a constant.
 



More resources:

1. [4 Reasons why var is considered obsolete](https://medium.com/javascript-in-plain-english/4-reasons-why-var-is-considered-obsolete-in-modern-javascript-a30296b5f08f)
2. [MDN docs: var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
3. David Flanagan, "JavaScript: The Definitive Guide", 7th Edition - pages 53-57