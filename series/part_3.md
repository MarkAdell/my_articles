# Yet another introduction to Functional Programming (Part Three)

Welcome to the third part of our series of articles on Functional Programming. In the previous part, we discussed pure functions. In this part, we will explore Immutability.

Be sure to check our previous parts:

- [Yet another introduction to Functional Programming (Part One)](https://github.com/MarkAdell/functional_programming_article/blob/main/series/part_1.md)
- [Yet another introduction to Functional Programming (Part Two)](https://github.com/MarkAdell/functional_programming_article/blob/main/series/part_2.md)

## Immutability

Immutability is the practice of not modifying data entities after they are created. When a change is required, a new data entity is created to hold the modified data, while the original data entity remains unchanged.

Immutability helps prevent bugs that arise when a developer assumes a data entity holds a specific value, when in reality, it has been changed elsewhere in the code.

Depending on the programming language you use, there may or may not be a way to enforce immutability, by having support for immutable variables and data structures. This is why I referred to immutability as a "practice", as in some cases, it will be your responsibility to avoid direct mutation (modification) of data entities.

To achieve immutability, we can follow these general principles, regardless of the programming language we use:
- Using constant variables if supported.
- Using immutable data structures if supported.
- Avoiding direct mutation to data entities.

Let's see some examples:

```javascript
// Bad: Variable is mutated.
let name = 'Mark';

name = 'DenMark';

// Better: New variable (data entity) is created to hold the updated value.
let name = 'Mark';

let newName = 'DenMark';

// Even better: Using constant variables to enforce immutability (A TypeError will be thrown if we reassigned name).
const name = 'Mark';

const newName = 'DenMark';
```

Please note that in JavaScript, the `const` keyword ensures that the variable cannot be reassigned. However, it does not make the value it holds immutable. For example:

```javascript
const numbers = [1, 2, 3];

numbers.push(4); // This is allowed.

console.log(numbers); // [1, 2, 3, 4]

numbers = [1, 2, 3, 4, 5]; // TypeError: Assignment to constant variable.
```

This is a case where it will be your responsibility to follow the "practice" of creating a new data entity to hold the new value, and avoid mutating the original one.

```javascript
const numbers = [1, 2, 3];

// Creating a new array by copying the old array and adding the new element 4.
const newNumbers = [...numbers, 4];

console.log(numbers); // [1, 2, 3]
console.log(newNumbers); // [1, 2, 3, 4]
```

The same principle applies to JavaScript objects:

```javascript
const person = {
    name: 'Mark'
};

// Creating a new object by copying the old object and adding the new age property.
const newPerson = {
    ...person,
    age: 13
};

console.log(person); // { name: 'Mark' }
console.log(newPerson); // { name: 'Mark', age: 13 }

// Even better: Enforcing Object immutability using Object.freeze()
const person = Object.freeze({
    name: 'Mark'
});

person.age = 13; // Fails silently.

console.log(person); // { name: 'Mark' }

const newPerson = {
    ...person,
    age: 13
};

console.log(newPerson); // { name: 'Mark', age: 13 }
```

I don't want to dive into more language-specific details as it is not the purpose of this article. The takeaway is, **enforce immutability when you can, otherwise, do your best following the practice of not mutating data entities**.

For many programming languages, there are either internal or external libraries that provide immutable data structures and utilities to achieve immutability. Some examples are:
- [immutable](https://www.npmjs.com/package/immutable) for JavaScript.
- [pyrsistent](https://pypi.org/project/pyrsistent/) for Python.
- [eclipse-collections](https://github.com/eclipse/eclipse-collections) for Java.
- [System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/) for C#.

Immutability doesn't stop at variables and data structures. Sometimes, it's also useful to make our classes immutable, such as Data Transfer Objects (DTOs), and it comes with its own benefits. As a final example (pun intended), let's see how we can build an immutable class in Java:

```java
final public class Person {
    private final String name;
    private final int age;
    private final List<String> hobbies;

    public Person(String name, int age, List<String> hobbies) {
        this.name = name;
        this.age = age;
        this.hobbies = Collections.unmodifiableList(hobbies);
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public List<String> getHobbies() {
        return hobbies;
    }
}
```

Note the following class properties:
- Class is declared as `final` to prevent inheritance.
- Class fields are declared as `final` to make them immutable.
- The `hobbies` list is made immutable by using `Collections.unmodifiableList()`.
- Class doesn't have any setter methods.

Let's wrap things up here. Immutability is a broad topic. We covered its basic fundamentals, and I hope I have made you curious to dive deeper.

## Conclusion

This concludes part three of our series. We discussed Immutability and how it helps you avoid a lot of unpredictable bugs. In the next part, we will cover First-class functions and Higher-order functions, helping you write more concise, readable, and reusable code. Stay tuned!
