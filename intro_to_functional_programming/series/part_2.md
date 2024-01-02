# Yet another introduction to Functional Programming (Part Two)

Welcome to the second part of our series of articles on Functional Programming. In the previous part, we gave an introduction and we discussed imperative vs declarative code. In this part, we will explore Pure Functions.

Be sure to check our previous parts:

- [Yet another introduction to Functional Programming (Part One)](https://github.com/MarkAdell/my_articles/blob/main/intro_to_functional_programming/series/part_1.md)

## Pure functions

Pure functions are the heart of functional programming, and they play a fundamental role in applying other functional programming concepts.

Pure functions are functions that have the following properties:
1. They don't cause side effects to inputs or the global state.
    - Making the code **Less prone to bugs**.
2. When called with the same input, they always return the same output (Referential transparency).
    - Making the code **Predictable**, **Testable**, **Cacheable**.
3. They only depend on their input to produce the output.
    - Making the code **Less prone to bugs**, **Testable**, **Composable**.

Let's see examples of impure functions violating each of these properties and then how to rewrite them to be pure.

### Causing side effects #1:

```javascript
// Impure function #1

let counter = 0;

function incrementCounter() {
    counter++;
}

incrementCounter();

console.log(counter); // 1
```

The previous function is not pure because it causes side effects by modifying the `counter` variable (global state).

Refactored into a pure function:

```javascript
// Pure function #1

let counter = 0;

function incrementCounter(counter) {
    return counter + 1;
}

let incrementedCounter = incrementCounter(counter);

console.log(incrementedCounter); // 1

console.log(counter); // 0
```

Instead of modifying the global variable, we passed the counter as an input and returned the incremented value.

### Causing side effects #2:

```javascript
// Impure function #2

function sum(a, b) {
    console.log('Hello world!');
    return a + b;
}
```

The previous function is not pure as it causes side effects by logging something to the console.

```javascript
// Pure function #2

console.log('Hello world!');

function sum(a, b) {
    return a + b;
}
```

By removing the `console.log`, the function no longer causes side effects. If you are so eager to greet the world, you can do it outside of this function.

### Causing side effects #3:

```javascript
// Impure function #3

const numbers = [1, 2, 3, 4, 5];

function doubleNumbers(numbers) {
    for (let i = 0; i < numbers.length; i++) {
        numbers[i] = 2 * numbers[i];
    }
}

doubleNumbers(numbers);

console.log(numbers) // [2, 4, 6, 8, 10]
```

The previous function is not pure because it causes side effects by modifying its input parameter.

Refactored into a pure function:

```javascript
// Pure function #3

const numbers = [1, 2, 3, 4, 5];

function doubleNumbers(numbers) {
    const result = [];

    for (let i = 0; i < numbers.length; i++) {
        result.push(2 * numbers[i]);
    }

    return result;
}

const doubledNumbers = doubleNumbers(numbers);

console.log(doubledNumbers) // [2, 4, 6, 8, 10]

console.log(numbers) // [1, 2, 3, 4, 5]
```

Instead of modifying the input, we created a new array `result` to store the updated values and returned it.

Please note that if arrays are passed by value in the programming language you use, it will be acceptable to modify the passed `numbers` array directly and return it, the function will be pure as it doesn't affect the original array.

### Not the same output for the same input:

```javascript
// Impure function #4

function isWeekend(weekendDays) {
    const currentDay = new Date().getDay();
    return weekendDays.includes(currentDay);
}

const weekendDays = [0, 6]; // Sunday and Saturday.

console.log(isWeekend(weekendDays)); // Might return true or false for the same input.
```

The previous function is not pure because it doesn't always return the same output for the same input, this happened because it doesn't depend fully on its input to produce the output, instead, it also depends on the internally generated current day.

Refactored into a pure function:

```javascript
// Pure function #4

function isWeekend(day, weekendDays) {
    return weekendDays.includes(day);
}

const currentDay = new Date().getDay();
const weekendDays = [0, 6]; // Sunday and Saturday.

console.log(isWeekend(currentDay, weekendDays)); // true if the given day is Sunday or Saturday, otherwise false.
```

Instead of making the function generate the current day internally, we passed the day as a parameter. By making the output fully depend on the input, we are now sure the function will always return the same output for the same input.

### Not fully depending on the input to produce output:

```javascript
// Impure function #5

let taxRate = 0.1;

function calculateTotalAmount(itemPrice) {
    return itemPrice + (itemPrice * taxRate);
}

const itemPrice = 100;

const totalPrice = calculateTotalAmount(itemPrice);

console.log(totalPrice); // 110
```

The previous function is not pure because it doesn't depend fully on the input to produce the output, instead, it also depends on an external variable `taxRate`.

There is a catch here, the function is not impure just because it depends on an external variable. It is impure because this external variable can be modified at anytime, which means the function is not guaranteed to always return the same output for the same input.

Refactored into a pure function:

```javascript
// Pure function #5

function calculateTotalAmount(price, taxRate) {
    return price + (price * taxRate);
}

const itemPrice = 100;
const taxRate = 0.1;

const totalPrice = calculateTotalAmount(itemPrice, taxRate);

console.log(totalPrice); // 110
```

Instead of depending on an external variable, we passed all the needed variables to the function so that it depends fully on its input to produce the output.

Another approach:

```javascript
// Pure function #5 second approach

const taxRate = 0.1;

function calculateTotalAmount(itemPrice) {
    return itemPrice + (itemPrice * taxRate);
}

const itemPrice = 100;

const totalPrice = calculateTotalAmount(itemPrice);

console.log(totalPrice); // 110
```

By declaring `taxRate` with `const` instead of `let`, making it immutable, it is guaranteed that the function always returns the same output for the same input. However, it is advisable to use the first approach, which is passing the `taxRate` as a parameter, as this makes the function more self-contained.

### When to use Pure Functions

Whenever possible! It is important to recognize that not all functions in real-world applications can be pure. Sometimes the whole purpose of a function is to do side effects or rely on external dependencies to return or compute a value, think of I/O operations. So, when should you use Pure Functions? Whenever you find yourself writing a function whose purpose is to perform a computation or transformation based on a value that you have, then it is a good candidate for a pure function.

## Conclusion

This concludes part two of our series. We discussed Pure Functions and the several benefits they add to our code. In the next part, we will cover Immutability, which is a practice that automatically helps you avoid a lot of unpredictable bugs. Stay tuned!
