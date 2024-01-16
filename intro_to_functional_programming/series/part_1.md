# Yet Another Introduction to Functional Programming (Part One)

In these series of articles, we will explore the fundamental principles of functional programming that you can utilize in your day-to-day work, regardless of the programming language you use.

There is a common misconception among beginners that one can only write pure functional programming code, or only stick to other paradigms like OOP. This is not true. One of the beauties of functional programming is that you can make use of it in any programming paradigm you use, and it will not fail to make your code more maintainable. And in the last article, we will show an example of how we can utilize these concepts within object-oriented programming code.

I decided to use JavaScript for most of the code examples because of its concise syntax and native support for some of the functional programming building blocks, such as treating functions as first-class citizens. However, it is likely that you can apply everything we will cover here in your preferred programming language.

## What is Functional Programming

Functional Programming is a programming paradigm that promotes writing code in a **declarative** rather than imperative manner and utilizes concepts such as **pure functions**, **immutability**, and **higher-order functions**, leading to code that is more maintainable and less prone to bugs.

We will explore each of these concepts, providing lots of code examples. Let's dive in!

## Imperative VS Declarative code

In imperative code, you write specific instructions to the compiler on **how** to compute a result, while in declarative code, you describe **what** is the result that you want to compute.

Let's see an example of imperative code that populates a new array with the even numbers from another array:

```javascript
// Imperative approach

function isEven(number) {
    return number % 2 === 0;
}

const numbers = [1, 2, 3, 4, 5, 6, 7, 8];

const evenNumbers = [];

for (let i = 0; i < numbers.length; i++) {
    if (isEven(numbers[i])) {
        evenNumbers.push(numbers[i]);
    }
}

console.log(evenNumbers); // [2, 4, 6, 8]
```

As you can see, we are giving specific instructions on how to compute the desired result. We manually implemented the filtering logic by looping through the array and populating the `evenNumbers` array based on a condition.

Now, let's see how to achieve the same result using declarative code:

```javascript
// Declarative approach

function isEven(number) {
    return number % 2 === 0;
}

function filter(array, predicate) {
  // implementation of the filtering logic
}

const numbers = [1, 2, 3, 4, 5, 6, 7, 8];

const evenNumbers = filter(numbers, isEven); // <-- the declarative code

console.log(evenNumbers); // [2, 4, 6, 8]
```

In the declarative approach, we described the desired outcome. We were like "Hey compiler, we want the `evenNumbers` array to hold the values of the `numbers` array after only including the even numbers".

Even if you are unaware of the inner implementation of the `filter` function, you will likely understand what is happening as the code is self-descriptive and reads like English. And this is the beauty of declarative code.

Please note that many programming languages provide built-in functions like `filter`. We will cover this later in the article when we discuss higher-order functions.

This is unrelated to functional programming, but we can make the code more concise using [arrow functions](https://www.w3schools.com/js/js_arrow_function.asp). Arrow functions provide a shorter syntax for creating function expressions and are supported in many programming languages, also known as *Lambda Expressions*.

```javascript
// Declarative approach using arrow functions

const numbers = [1, 2, 3, 4, 5, 6, 7, 8];

function filter(array, predicate) {
  // implementation of the filtering logic
}

const evenNumbers = filter(numbers, number => number % 2 === 0);

console.log(evenNumbers); // [2, 4, 6, 8]
```

Moving forward, we will use arrow functions to pass functions around in the code examples.

Let's see another example:

```javascript
// Imperative approach

const numbers = [1, 2, 3, 4, 5];

let max = numbers[0];

for (let i = 1; i < numbers.length; i++) {
    if (numbers[i] > max) {
        max = numbers[i];
    }
}

console.log(max); // 5

// Declarative approach

const numbers = [1, 2, 3, 4, 5];

const max = Math.max(...numbers);

console.log(max); // 5
```

## Conclusion

This concludes part one of our series. We discussed the difference between imperative and declarative code and how declarative code is more readable and easier to reason about. In the next part, we will cover Pure Functions, which are considered the heart of functional programming and play a fundamental role in applying other functional programming concepts. Stay tuned!