---
title: Array Method Examples
description: How to manipulate and use arrays in Javascript
published: true
date: 2022-09-16T21:39:35.886Z
tags: javascript, arrays, methods, foreach, array.isarray, array.foreach, map, every, some, filter
editor: markdown
dateCreated: 2022-09-16T21:39:35.886Z
---

# Javascript Arrays

<br>

## **Checking if an Object is an array using `Array.isArray()` method**

````javaqscript
const example = ['example1', 'example2', 'example3', 'example4'];

if (Array.isArray(example)) {
    // Code to execute if example is in fact an array
}
````

<br>

## **Loop over every element in an array, in order**

````javascript
const example = ['example1', 'example2', 'example3', 'example4'];

for (const ex of example) {
    console.log(example);
}
````

<br>


## **Iterating over an Array in a functional way using `Array.forEach()`**

> You supply a function, which is called once for each element in the array, then passed three potentially useful parameters(the element, the element's index, and the original array).

````javascript
const example = ['example1', 'example2', 'example3', 'example4'];

example.forEach(function(example, index, array) {
    console.log(example);
}
````
**Condensed version of the above code**

````javascript
example.forEach(example => console.log(example));
````

<br>

## **Basic for loop with a counter**

````javascript
const example = ['example1', 'example2', 'example3', 'example4'];

for (let i = 0; i < example.length; ++i) {
    console.log(example[i]);
}
````

<br>

# Methods for Functional Array Processing

**Change every array element: `map()`**

**See if all elements meet a specific condition: `every()`**

**See if atleast one element meets a specific condition: `some()`**

**Find array elements matching your criteria: `filter()`**

**Reorder an array: `sort()`**

**Use all values of an array in one calculation: `reduce()`**

<br>

# Checking if Two Arrays are Equal

Best way to accomplish this is a basic for loop with a counter, stepping through both arrays at the same time and comparing each element in the process.

````javascript
function areArraysEqual(exampleA, exampleB) {
    if (!Array.isArray(exampleA) || !Array.isArray(exampleB)) {
        return false;
    } else if (exampleA === exampleB) {
        return true;
    } else if (exampleA.length !== exampleB.length) {
        return false;
    } else {
        for (let i = 0; i < exampleA.length; ++i) {
            if (exampleA[i] !== exampleB[i]) return false;
        }
        return true;
    }
}
````

<br>

# Breaking Down an Array into Separate Variables

Use array destructuring syntax to assign multiple variables at a time.

**Example**

````javascript
const example = ['example1', 'example2', 'example3', 'example4'];

const ['value1', 'value2', 'value3', 'value4', 'value5'] = example;

console.log(value3); //example3
````

<br>

# Passing an Array to a function that Expects a List of Values

Use the spread operator to expand your array

Example with `Math.max()` method

````javascript
const numbers = [2, 42, 5, 304, 1, 13];

// This syntax is not allowed. The result is NaN.
const maximumFail = Math.max(numbers);

// But this works, thanks to the spread operator. (The answer is 304.)
const maximum = Math.max(...numbers);
````

<br>

>The spread operator unfolds an array into a list of elements

<br>

# Extracting Array Items that Meet a Specific Criteria

You want to find all the items in an array that match a certain condition, and copy them to a new array.

**Using the `Array.filter()` method runs a test on every item:**

````javascript
function startsWithE(animal) {
    return animal[0].toLowerCase() === 'e';
}
const animals = ['elephant', 'tiger', 'emu', 'zebra', 'cat', 'dog',
'eel', 'rabbit', 'goose', 'earwig'];

const animalsE = animals.filter(startsWithE);
console.log(animalsE); // ["elephant", "emu", "eel", "earwig"]
````

Same code in condensed form:

````javascript
const animals = ['elephant', 'tiger', 'emu', 'zebra', 'cat', 'dog',
'eel', 'rabbit', 'goose', 'earwig'];

const animalsE = animals.filter(animal => animal[0].toLowerCase() === 'e');
````

>The filter function checks that each item begins with the letter e. But you could just as easily grab numbers that fall in a certain range, or objects that have certain property values.

<br>

# Emptying an Array

Set the property of your array to 0:

````javascript
const numbers = [2, 42, 5, 304, 1, 13];
numbers.length = 0;
````

<br>

# Removing Duplicate Values

Ensure that every value in your array is unique by removing the
duplicates.

Create a new `Set` object and fill it with your array. The `Set` object will discard duplicates automatically. Then, convert the `Set` object back to an array:

````javascript
const numbersWithDuplicates = [2, 42, 5, 42, 304, 1, 13, 2, 13];
// Create a Set with unique values (the duplicate 42, 2, and 13 are discarded)

const uniqueNumbersSet = new Set(numbersWithDuplicates);

// Turn the Set back into an array (now with 6 items)
const uniqueNumbersArray = Array.from(uniqueNumbersSet);
````

Compressed down using the spread operator:

````javascript
const numbersWithDuplicates = [2, 42, 5, 42, 304, 1, 13, 2, 13];

const uniqueNumbers = [...new Set(numbersWithDuplicates)];
````

>The `Set` object is a special type of collection that ignores duplicate values. It also works as a quick and efficient way to remove duplicates from an array

<br>

# Searching Through an Array for Exact Matches

Use one of the array searching methods: `indexOf()`, `lastIndexOf()`, or `includes()`:

````javascript
const animals = ['dog', 'cat', 'seal', 'elephant', 'walrus', 'lion'];

console.log(animals.indexOf('elephant')); // 3

console.log(animals.lastIndexOf('walrus')); // 4

console.log(animals.includes('dog')); // true
````

>This technique only works for primitive values (typically numbers, strings, and Boolean values).

<br>

# Validating Array Contents

Use the `Array.every()` method to check that every element passes a given test. For example, the following code checks to ensure that every element in the array consists of alphabetic characters using a regular expression:

````javascript
// The testing function
function containsLettersOnly(element) {
    const textExp = /^[a-zA-Z]+$/;
    return textExp.test(element);
}

// Test an array
const mysteryItems = ['**', 123, 'aaa', 'abc', '-', 46, 'AAA'];

let result = mysteryItems.every(containsLettersOnly);
console.log(result); // false

// Test another array
const mysteryItems2 = ['elephant', 'lion', 'cat', 'dog'];

result = mysteryItems2.every(containsLettersOnly);
console.log(result); // true
````

Or, use the Array.some() method to ensure that at least one of the elements passes the test. As an example, the following code checks to ensure that at least one of the array elements is an alphabetical string:

````javascript
const mysteryItems = new Array('**', 123, 'aaa', 'abc', '-', 46, 'AAA');

// testing function
function testValue (element) {
    const textExp = /^[a-zA-Z]+$/;
    return textExp.test(element);
}

// run test
const result = mysteryItems.some(testValue);
console.log(result); // true
````