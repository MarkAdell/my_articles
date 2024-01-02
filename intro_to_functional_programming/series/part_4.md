# Yet another introduction to Functional Programming (Part Four)

Welcome to the fourth part of our series of articles on Functional Programming. In the previous part, we discussed Immutability. In this part, we will explore First-class functions and Higher-order functions.

Be sure to check our previous parts:

- [Yet another introduction to Functional Programming (Part One)](https://github.com/MarkAdell/my_articles/blob/main/intro_to_functional_programming/series/part_1.md)
- [Yet another introduction to Functional Programming (Part Two)](https://github.com/MarkAdell/my_articles/blob/main/intro_to_functional_programming/series/part_2.md)
- [Yet another introduction to Functional Programming (Part Three)](https://github.com/MarkAdell/my_articles/blob/main/intro_to_functional_programming/series/part_3.md)

## First-class functions

First-class functions refer to the ability of functions to be treated as values. This means you can assign functions to variables, pass them as arguments to other functions, and return them as values from other functions.

First-class functions serve as the foundation for techniques like higher-order functions and function composition in functional programming.

Let's see some examples:

```javascript
// Assigning functions to variables.
const sum = function(a, b) {
    return a + b;
}

console.log(sum(3, 4)); // 7

// Passing functions as arguments to other functions.
function calculate(operation, a, b) {
    return operation(a, b);
}

console.log(calculate(sum, 3, 4)); // 7

console.log(
    calculate(function(a, b) {
        return a * b
    }, 3, 4)
); // 12

console.log(
    calculate((a, b) => a - b, 3, 4)
); // -1

// Returning functions from other functions.
function getOperation(type) {
    if (type === 'add') {
        return function(a, b) {
            return a + b;
        }
    }

    return function(a, b) {
        return a - b;
    }
}

const operation = getOperation('add');

console.log(operation(3, 4)); // 7
```

We are ready now to move on to the last concept we'll explore today: Higher-order functions.

## Higher-order functions

Higher-order functions are functions that can take one or more functions as arguments or return functions as their results.

One of several benefits of higher-order functions is that they enable code reusability. Instead of writing similar logic, such as filtering, multiple times, you can encapsulate it in a higher-order function once and pass different functions as arguments to achieve different behaviors.

Many programming languages provide built-in higher-order functions for manipulating lists or collections without the need for loops. Making the code more concise, reusable, and readable. Some of the common higher-order functions for list manipulation are:
- **Map**: Applies a given function to each list element, returning a new list with the transformed values.
- **Filter**: Filters list elements based on a given predicate function (a function that returns a bool), returning a new list with the filtered elements.
- **Reduce**: Combines list elements into a single value using a given accumulator function, simplifying computations like summing or finding the maximum.
- **Find**: Searches for a specific element in a list based on a given predicate function.

And the list goes on.

Let's see a code example for filtering an array and explain the benefits of using higher-order functions:

```javascript
// Using the iterative approach (imperative).

const numbers = [1, 2, 3, 4, 5, 6, 7, 8];

const evenNumbers = [];

for (let i = 0; i < numbers.length; i++) {
    if (number[i] % 2 == 0) {
        evenNumbers.push(numbers[i]);
    }
}

console.log(evenNumbers); // [2, 4, 6, 8]

// Using a higher-order function (declarative).

const numbers = [1, 2, 3, 4, 5, 6, 7, 8];

const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers); // [2, 4, 6, 8]
```

Benefits of writing this code using the `filter` higher-order function:
- It's more concise because we achieved the same task using fewer lines of code.
- It's more readable because it's declarative, we describe **what** we want, not **how** to do it.
- It's more reusable because the main filtering logic is implemented once inside the `filter` function, allowing it to be used for different filtering scenarios based on the filtering criteria we provide.
- It's pure. Higher-order functions are often implemented to be pure, so we get all the nice benefits of pure functions.

So every time we use the iterative, imperative approach, we lose most of these benefits, along with some added drawbacks, such as:
- The risk of introducing bugs.
- The risk of writing unreadable code.
- The risk of introducing performance issues.

### Examples using higher-order functions

Let's see examples of using some of the built-in JavaScript higher-order functions:

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const squaredNumbers = numbers.map(number => number * number); // [1, 4, 9, 16, 25, 36]

const numbersLessThanSix = numbers.filter(number => number < 6); // [1, 2, 3, 4, 5]

const firstEvenNumber = numbers.find(number => number % 2 === 0); // 2

const hasNegativeNumbers = numbers.some(number => number < 0); // false

const initialValue = 0;
const sum =  numbers.reduce((accumulator, currentValue) => accumulator + currentValue, initialValue); // 21
```

### Composing higher-order functions

Remember when we said that higher-order functions are pure and this gives us the benefits of pure functions? One of these benefits is composability, it means that we can safely compose these functions together, by letting the output of one function be the input of another function. This is made possible because pure functions always get an input and produce an output, and output only depends on the input.

Let's write code that gets us the sum of odd numbers after multiplying each odd number by three:

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const result = numbers
    .filter(number => number % 2 != 0)
    .map(number => number * 3)
    .reduce((a, b) => a + b, 0);

console.log(result); // 27
```

We chained the three functions to compute our desired result. The output of the `filter` becomes the input of the `map`, and the output of the `map` becomes the input of the `reduce`.

Please note that chaining is one form of function composition.

### Implementing higher-order functions

Now to the fun part, let's see how we can implement these higher-order function ourselves. We will implement `map`, `filter`, `some`, and a bonus function called `countOccurrences` which doesn't have a built-in equivalent in JavaScript.

```javascript
function map(array, mapper) {
    const result = [];

    for (let i = 0; i < array.length; i++) {
        result.push(mapper(array[i]));
    }

    return result;
}

const squaredNumbers = map([1, 2, 3, 4], number => number * number); 

console.log(squaredNumbers); // [1, 4, 9, 16]

// ------------------------

function filter(array, predicate) {
    const result = [];

    for (let i = 0; i < array.length; i++) {
        if (predicate(array[i])) {
            result.push(array[i]);
        }
    }

    return result;
}

const evenNumbers = filter([1, 2, 3, 4], number => number % 2 === 0);

console.log(evenNumbers); // [2, 4]

// ------------------------

function some(array, predicate) {
    for (let i = 0; i < array.length; i++) {
        if (predicate(array[i])) {
            return true;
        }
    }

    return false;
}

const hasNegativeNumbers = some([-1, 0, 1, 2], number => number < 0);

console.log(hasNegativeNumbers); // true

// ------------------------

function countOccurrences(array, predicate) {
    let counter = 0;

    for (let i = 0; i < array.length; i++) {
        if (predicate(array[i])) {
            counter += 1;
        }
    }

    return counter;
}

const evenNumbersCount = countOccurrences([1, 2, 3, 4], number => number % 2 == 0);

console.log(evenNumbersCount); // 2
```

Please note how they are all implemented to be pure.

### Higher-order functions exercise

Exercise time! Try to implement a higher-order function called `findLast` that accepts an array and a predicate function and returns the last element in the array that satisfies the given predicate, or `undefined` otherwise. This is how it will be used:

```javascript
const lastNumberBiggerThanOne = findLast([4, 9, 5, 6, 2], number => number > 1);

console.log(lastNumberBiggerThanOne); // 2
```

[Here](https://gist.github.com/MarkAdell/05afa2f6f873694c21eff85f49a9552d) is a possible solution to the exercise.

### Higher-order functions real life example

Let's see a more real life example for using higher-order functions, applying different discounts to a shopping cart:

```javascript
const cartItems = [
    { name: "Item 1", price: 10 },
    { name: "Item 2", price: 20 },
    { name: "Item 3", price: 30 },
];

function applyDiscount(item, discount) {
    const discountedPrice = item.price - (item.price * discount);
    return { ...item, price: discountedPrice }; // Copying the item object to another object and overriding the price value.
}

const regularDiscount = 0.1; // 10% discount.
const specialDiscount = 0.5; // 50% discount.

const regularCustomersCart = cartItems.map(item => applyDiscount(item, regularDiscount));
const specialCustomersCart = cartItems.map(item => applyDiscount(item, specialDiscount));

console.log(regularCustomersCart); // [{ name: "Item 1", price: 9 }, { name: "Item 2", price: 18 }, { name: "Item 3", price: 27 }]
console.log(specialCustomersCart); // [{ name: "Item 1", price: 5 }, { name: "Item 2", price: 10 }, { name: "Item 3", price: 15 }]
```

**It is important** to note that if `applyDiscount` mutates its input by modifying the item price directly, the `map` function will mutate the entire `cartItems` array, which we don't want. Therefore, it is crucial that the callbacks we pass to our higher-order functions are implemented to be pure.

As a final note, you may initially find yourself somewhat resistant to using higher-order functions in your code. It is understandable because all of us got introduced to loops first and became accustomed to using them. However, I can assure you that with little practice and commitment to using higher-order functions whenever possible, it will become second nature and you will start to appreciate their power and elegance.

## Conclusion

This concludes part four of our series. We discussed First-class functions and Higher-order functions and how they help you write more concise, readable, and reusable code. In the next and final part, we will show how we can utilize all the functional programming concepts that we covered within object-oriented programming code. Stay tuned!
