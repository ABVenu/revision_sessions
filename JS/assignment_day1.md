
## JavaScript Fundamentals Assignments & Interview Questions

### Section 1: Direct Implementation Assignments 

For these assignments, write JavaScript code to directly implement the requirements. Focus on using variables, data types, control flow, loops, arrays, and strings.

**Assignment 1: Variable Declaration, Type Coercion, and Basic Output**

1.  Declare a constant variable `productName` and assign it the string value "Smart Watch".
2.  Declare a `let` variable `unitPrice` and assign it the number `150.75`.
3.  Declare a `let` variable `quantity` and assign it the number `3`.
4.  Calculate `totalCost` by multiplying `unitPrice` and `quantity`.
5.  Try to add `productName` and `totalCost`. Store the result in a variable `combinedInfo`.
6.  Log the `totalCost` to the console.
7.  Log `combinedInfo` to the console, and also log its `typeof`.
8.  Declare a `let` variable `discountPercentage` and assign it the string `"10"`.
9.  Calculate the `discountAmount` by multiplying `totalCost` with `discountPercentage` (you'll observe implicit coercion here).
10. Log the `discountAmount` and its `typeof` to the console.

**Assignment 2: String Manipulation and Validation**

Given the string `sentence = "  JavaScript is an amazing language!   "`.

1.  Remove any leading or trailing whitespace from `sentence` and store the result in `trimmedSentence`.
2.  Convert `trimmedSentence` to all uppercase letters and store it in `upperCaseSentence`.
3.  Extract the word "amazing" from `trimmedSentence` using `slice()` and store it in `extractedWord`.
4.  Check if `trimmedSentence` includes the word "language". Store the boolean result in `includesLanguage`.
5.  Check if `trimmedSentence` starts with "Java". Store the boolean result in `startsWithJava`.
6.  Log `trimmedSentence`, `upperCaseSentence`, `extractedWord`, `includesLanguage`, and `startsWithJava` to the console.

**Assignment 3: Array Filtering and Summation (using Loops)**

You are given an array of numbers: `data = [12, 5, 20, 8, 15, 30, 7, 25]`

1.  Create an empty array called `evenNumbers`.
2.  Using a `for` loop, iterate through the `data` array.
3.  Inside the loop, check if each number is even. If it is, add it to the `evenNumbers` array using `push()`.
4.  After the loop, calculate the sum of all numbers in the `evenNumbers` array. Store the sum in `sumOfEvens`. Use another `for` loop for this.
5.  Log both `evenNumbers` and `sumOfEvens` to the console.

**Assignment 4: Conditional Access Control**

Imagine a simple user access system. You have the following `let` variables:
`isAuthenticated = true;`
`userRole = "admin";`
`hasPremiumSubscription = false;`

Write `if/else if/else` statements to determine the user's access level and print a corresponding message.

  * If `isAuthenticated` is `true` AND `userRole` is "admin", print: "Welcome, Administrator\! Full access granted."
  * Else if `isAuthenticated` is `true` AND `hasPremiumSubscription` is `true`, print: "Welcome, Premium User\! Enjoy exclusive content."
  * Else if `isAuthenticated` is `true`, print: "Welcome, Regular User\! Limited access."
  * Else (if `isAuthenticated` is `false`), print: "Please log in to access the system."

**Assignment 5: Pattern Generation with Loops**

Use a `for` loop to generate a string that looks like a staircase pattern. The string should be built line by line, separated by newline characters (`\n`).

Example output for `rows = 4`:

```
#
##
###
####
```


-----

### Section 2: Interview-Type Questions (Conceptual & Knowledge Check)

These questions are designed to test your understanding of core JavaScript concepts. Answer them thoroughly with explanations and, where appropriate, small illustrative examples.

**Question 1: Variable Scoping and Hoisting**

Explain the key differences between `var`, `let`, and `const` declarations in JavaScript. Focus on:

  * **Scope:** Describe "function scope" versus "block scope" with examples for each variable type.
  * **Hoisting:** How does hoisting work for each? What is the "Temporal Dead Zone" and which variable types are affected by it?
  * **Redeclaration and Reassignment:** Can each be redeclared or reassigned in the same scope?
    Provide a concise summary of when you would typically use `let` versus `const`.

**Question 2: Type Equality and Coercion**

Describe the fundamental difference between the `==` (loose equality) and `===` (strict equality) operators in JavaScript.

  * When would `==` return `true` while `===` returns `false`? Give a concrete code example.
  * Why is it generally recommended to use `===` over `==`?
  * Explain a scenario where implicit type coercion might lead to unexpected results, beyond just `==`.

**Question 3: Primitive vs. Reference Types - Copying Behavior**

JavaScript distinguishes between primitive and reference data types.

  * Explain how values are typically stored in memory for primitive types (e.g., `number`, `string`) versus reference types (e.g., `object`, `array`).
  * How does this storage mechanism affect the behavior when you copy a value from one variable to another for each type?
  * Provide two small code examples, one demonstrating "copy by value" for a primitive type, and another demonstrating "copy by reference" for a reference type, showing how changes to one variable affect (or don't affect) the other.

**Question 4: Truthiness and Falsiness**

What are "truthy" and "falsy" values in JavaScript?

  * List all the specific values in JavaScript that are considered "falsy."
  * Explain how these values behave when evaluated in a boolean context (e.g., within an `if` statement or with logical operators).
  * How can the double negation operator (`!!`) be used in relation to truthy/falsy values? Provide an example.

**Question 5: Short-Circuiting Operators in Detail**

Explain the short-circuiting behavior of the `||` (Logical OR), `&&` (Logical AND), and `??` (Nullish Coalescing) operators in JavaScript.

  * For each operator, describe what value it returns (it's not always just `true` or `false`).
  * Provide a practical use case for each operator.
  * Highlight the key difference between `||` and `??`, illustrating with an example where `??` would be the more appropriate choice.

-----