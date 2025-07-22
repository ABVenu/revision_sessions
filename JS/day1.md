
## Day 1: JavaScript Fundamentals Revision - Detailed Notes (Updated)

This comprehensive session is designed to solidify your understanding of JavaScript's foundational concepts, from variable handling and data types to control flow, essential array operations, and now, string manipulations. Each topic is broken down with clear explanations and key considerations.

-----

### 1\. Variables & Declarations

Variables are containers for storing data values. JavaScript offers three primary keywords for declaring them, each with distinct behaviors regarding scope, hoisting, and mutability.

**Topics:**

  * **`var`, `let`, `const` — Redeclaration, Reassignment, Scoping**

      * **`var`**:
          * **Scope**: **Function-scoped**. If declared inside a function, it's only accessible within that function. If declared outside any function, it's global.
          * **Redeclaration**: **Allowed**. You can declare the same `var` variable multiple times in the same scope without error.
            ```javascript
            var x = 10;
            var x = 20; // Allowed
            console.log(x); // 20
            ```
          * **Reassignment**: **Allowed**. You can change the value of a `var` variable after its initial declaration.
          * **Hoisting**: `var` declarations are **hoisted** to the top of their function or global scope. They are initialized with `undefined` during the creation phase, meaning you can access them before their actual declaration line without a `ReferenceError`.
            ```javascript
            console.log(myVar); // undefined (due to hoisting)
            var myVar = "Hello";
            console.log(myVar); // Hello
            ```
      * **`let`**:
          * **Scope**: **Block-scoped**. It's limited to the block (e.g., `if` statement, `for` loop, or any `{}` code block) in which it's defined.
          * **Redeclaration**: **Not allowed** in the same scope. Attempting to redeclare a `let` variable will result in a `SyntaxError`.
            ```javascript
            let y = 10;
            // let y = 20; // SyntaxError: 'y' has already been declared
            y = 20; // Allowed (reassignment)
            console.log(y); // 20
            ```
          * **Reassignment**: **Allowed**. You can change the value of a `let` variable.
          * **Hoisting**: `let` declarations are also hoisted, but they are *not initialized*. They enter a **Temporal Dead Zone (TDZ)** from the start of their block until their declaration is processed. Accessing a `let` variable within its TDZ will result in a `ReferenceError`.
            ```javascript
            // console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
            let myLet = "World";
            console.log(myLet); // World
            ```
      * **`const`**:
          * **Scope**: **Block-scoped**, similar to `let`.
          * **Redeclaration**: **Not allowed** in the same scope.
          * **Reassignment**: **Not allowed**. A `const` variable must be initialized at declaration and its value cannot be changed afterwards.
            ```javascript
            const z = 30;
            // z = 40; // TypeError: Assignment to constant variable.
            // const z = 50; // SyntaxError: 'z' has already been declared
            ```
          * **Important Note for Objects/Arrays**: While the *reference* itself cannot be reassigned, the *contents* of an object or array declared with `const` *can* be modified.
            ```javascript
            const myObject = { name: "Alice" };
            myObject.name = "Bob"; // Allowed - modifying the object's property
            console.log(myObject); // { name: "Bob" }

            // myObject = { age: 30 }; // TypeError: Assignment to constant variable. (reassigning the reference)
            ```
          * **Hoisting**: Similar to `let`, `const` declarations are hoisted but are in a TDZ until initialized, leading to a `ReferenceError` if accessed prematurely.

  * **Block Scope vs Function Scope**

      * **Function Scope**: Variables declared with `var` are accessible throughout the entire function in which they are declared, regardless of nested blocks.
        ```javascript
        function exampleVarScope() {
            if (true) {
                var funcVar = "I am function scoped";
            }
            console.log(funcVar); // "I am function scoped" (accessible outside the if block)
        }
        exampleVarScope();
        // console.log(funcVar); // ReferenceError: funcVar is not defined (not accessible globally)
        ```
      * **Block Scope**: Variables declared with `let` and `const` are only accessible within the specific block (defined by `{}`) where they are declared.
        ```javascript
        function exampleLetConstScope() {
            if (true) {
                let blockLet = "I am block scoped (let)";
                const blockConst = "I am block scoped (const)";
                console.log(blockLet); // "I am block scoped (let)"
                console.log(blockConst); // "I am block scoped (const)"
            }
            // console.log(blockLet); // ReferenceError: blockLet is not defined
            // console.log(blockConst); // ReferenceError: blockConst is not defined
        }
        exampleLetConstScope();
        ```

  * **Default values and declaration rules**

      * Variables declared with `var` or `let` without an initial value are automatically assigned the value `undefined`.
        ```javascript
        let unassignedLet;
        var unassignedVar;
        console.log(unassignedLet); // undefined
        console.log(unassignedVar); // undefined
        ```
      * Variables declared with `const` **must** be initialized at the time of declaration. Failing to do so will result in a `SyntaxError`.
        ```javascript
        // const mustBeInitialized; // SyntaxError: Missing initializer in const declaration
        ```

  * **Variable Naming Best Practices**

      * **`camelCase`**: The standard convention for variable and function names (e.g., `firstName`, `calculateTotal`).
      * **Descriptive Names**: Choose names that clearly indicate the variable's purpose or content (e.g., `customerName` instead of `cn`).
      * **Avoid Single Letters**: Unless it's a loop counter (`i`, `j`, `k`), avoid single-letter variable names for clarity.
      * **Keywords**: Do not use reserved JavaScript keywords (e.g., `if`, `for`, `function`) as variable names.

  * **Global variables and implicit globals**

      * **Global Variables**: Variables declared outside of any function or block, or explicitly attached to the global object (`window` in browsers, `global` in Node.js), are accessible from anywhere in the code.
        ```javascript
        var globalVar = "I am global (var)"; // Global scope
        let globalLet = "I am global (let)"; // Global scope
        const globalConst = "I am global (const)"; // Global scope

        function accessGlobals() {
            console.log(globalVar);
            console.log(globalLet);
            console.log(globalConst);
        }
        accessGlobals();
        ```
      * **Implicit Globals**: In **non-strict mode**, assigning a value to a variable that has not been explicitly declared with `var`, `let`, or `const` will automatically create a global variable. This is a common source of bugs and is **strongly discouraged**.
        ```javascript
        // In non-strict mode:
        function createImplicitGlobal() {
            implicitGlobal = "I am an implicit global"; // No var/let/const
        }
        createImplicitGlobal();
        console.log(implicitGlobal); // "I am an implicit global"

        // In strict mode (see section 12), this would throw a ReferenceError.
        ```

-----

### 2\. Data Types

JavaScript values are categorized into two main types: Primitive and Reference. This distinction is crucial for understanding how values are stored, copied, and compared.

**Topics:**

  * **Primitive Types**: Represent single, immutable values. When you assign a primitive value to a variable or pass it to a function, a new copy of that value is created.

      * `string`: Represents textual data. Enclosed in single quotes (`''`), double quotes (`""`), or backticks (`` ` `` for template literals).
        ```javascript
        let name = "John Doe";
        let message = `Hello, ${name}!`; // Template literal
        ```
      * `number`: Represents both integer and floating-point numbers. JavaScript uses double-precision 64-bit format.
        ```javascript
        let age = 30;
        let price = 99.99;
        let largeNum = 1.23e+5; // 123000
        ```
      * `boolean`: Represents a logical entity and can have only two values: `true` or `false`.
        ```javascript
        let isActive = true;
        let hasPermission = false;
        ```
      * `null`: Represents the intentional absence of any object value. It's a primitive value.
        ```javascript
        let selectedUser = null; // No user selected
        ```
      * `undefined`: Represents a variable that has been declared but has not yet been assigned a value, or a missing function argument.
        ```javascript
        let declaredButNotAssigned;
        console.log(declaredButNotAssigned); // undefined
        ```
      * `symbol`: Introduced in ES6 (ECMAScript 2015). Symbols are unique and immutable values, primarily used as unique property keys for objects to avoid name clashes.
        ```javascript
        const id1 = Symbol('id');
        const id2 = Symbol('id');
        console.log(id1 === id2); // false (each Symbol is unique)
        ```
      * `bigint`: Introduced in ES2020. Represents integers with arbitrary precision, meaning they can store numbers larger than `2^53 - 1` (the maximum safe integer for `number` type). Appended with `n`.
        ```javascript
        const largeInteger = 9007199254740991n; // This is a BigInt
        const anotherBigInt = BigInt("12345678901234567890");
        ```

  * **Reference Types**: Represent values that are stored as objects in memory. When you assign a reference type to a variable or pass it to a function, only the *reference* (memory address) to the object is copied, not the object itself.

      * `object`: The most fundamental reference type. A collection of key-value pairs (properties).
        ```javascript
        let person = {
            firstName: "Jane",
            lastName: "Doe",
            age: 25
        };
        ```
      * `array`: A special type of object used for storing ordered collections of values.
        ```javascript
        let colors = ["red", "green", "blue"];
        let mixed = [1, "hello", true, { id: 1 }];
        ```
      * `function`: Functions are first-class objects in JavaScript, meaning they can be assigned to variables, passed as arguments, and returned from other functions.
        ```javascript
        function greet(name) {
            return `Hello, ${name}!`;
        }
        let sayHello = greet; // Assigning the function to a variable
        ```

  * **`typeof` quirks (`typeof null === 'object'`)**

      * The `typeof` operator returns a string indicating the type of its operand.
      * **The `typeof null === 'object'` is a well-known, long-standing bug in JavaScript**. It's a historical artifact that remains for backward compatibility. While `null` is conceptually a primitive value, `typeof` incorrectly reports it as `'object'`.
      * Other `typeof` results:
        ```javascript
        console.log(typeof "hello");     // "string"
        console.log(typeof 123);         // "number"
        console.log(typeof true);        // "boolean"
        console.log(typeof undefined);   // "undefined"
        console.log(typeof Symbol('a')); // "symbol"
        console.log(typeof 10n);         // "bigint"
        console.log(typeof {});          // "object"
        console.log(typeof []);          // "object" (arrays are objects)
        console.log(typeof function(){});// "function" (functions are callable objects)
        ```

  * **Copy by value vs copy by reference**

      * **Copy by Value (Primitives)**: When you assign a primitive value from one variable to another, a completely independent copy of that value is created. Changes to one variable do not affect the other.
        ```javascript
        let a = 10;
        let b = a; // b gets a copy of the value 10
        b = 20;
        console.log(a); // 10 (a is unchanged)
        console.log(b); // 20
        ```
      * **Copy by Reference (Objects/Arrays/Functions)**: When you assign a reference type from one variable to another, both variables end up pointing to the *same object in memory*. Changes made through one variable will be visible through the other.
        ```javascript
        let obj1 = { value: 10 };
        let obj2 = obj1; // obj2 gets a copy of the reference (memory address) to the same object
        obj2.value = 20; // Modifying the object through obj2
        console.log(obj1.value); // 20 (obj1 also reflects the change)
        console.log(obj2.value); // 20

        // To create a true copy of an object/array (shallow copy), you need specific methods
        // e.g., for shallow copy: let obj3 = { ...obj1 }; or let arr2 = [...arr1];
        ```

-----

### 3\. Type Conversion & Coercion

JavaScript often needs to convert values from one type to another. This can happen explicitly (you tell it to) or implicitly (JavaScript does it automatically).

**Topics:**

  * **Explicit Conversion (Type Casting)**: You explicitly use functions or methods to convert a value's type.

      * `String()`: Converts a value to its string representation.
        ```javascript
        console.log(String(123));      // "123"
        console.log(String(true));     // "true"
        console.log(String(null));     // "null"
        console.log(String(undefined));// "undefined"
        console.log(String({}));       // "[object Object]"
        console.log(String([]));       // "" (empty string)
        ```
      * `Number()`: Converts a value to its numeric representation.
        ```javascript
        console.log(Number("123"));    // 123
        console.log(Number("Hello"));  // NaN (Not-a-Number)
        console.log(Number(true));     // 1
        console.log(Number(false));    // 0
        console.log(Number(null));     // 0
        console.log(Number(undefined));// NaN
        console.log(Number(""));       // 0
        ```
      * `Boolean()`: Converts a value to its boolean representation (`true` or `false`).
        ```javascript
        console.log(Boolean(1));       // true
        console.log(Boolean(0));       // false
        console.log(Boolean("hello")); // true
        console.log(Boolean(""));      // false
        console.log(Boolean(null));    // false
        console.log(Boolean(undefined));// false
        console.log(Boolean(NaN));     // false
        console.log(Boolean({}));      // true
        console.log(Boolean([]));      // true
        ```
      * `parseInt()`: Parses a string argument and returns an integer. It stops parsing when it encounters a non-numeric character.
        ```javascript
        console.log(parseInt("100px")); // 100
        console.log(parseInt("  12.34")); // 12
        console.log(parseInt("px100")); // NaN
        ```
      * `parseFloat()`: Parses a string argument and returns a floating-point number.
        ```javascript
        console.log(parseFloat("12.34px")); // 12.34
        console.log(parseFloat("  3.14")); // 3.14
        ```

  * **Implicit Coercion (Type Coercion)**: JavaScript automatically converts types when operations are performed on values of different types.

      * **With `+` (Addition vs. Concatenation)**:
          * If **any** operand is a string, the other operand is converted to a string, and the result is string concatenation.
          * Otherwise, both operands are converted to numbers, and the result is numeric addition.
        <!-- end list -->
        ```javascript
        console.log(5 + "5");    // "55" (number 5 converted to string "5")
        console.log("5" + 5);    // "55"
        console.log(5 + 5);      // 10
        console.log(true + 1);   // 2 (true converted to 1)
        console.log(null + 5);   // 5 (null converted to 0)
        console.log(undefined + 5); // NaN (undefined converted to NaN)
        ```
      * **With `-`, `*`, `/`, `%` (Numeric Operations)**:
          * All operands are converted to numbers. If a conversion results in `NaN`, the operation result will be `NaN`.
        <!-- end list -->
        ```javascript
        console.log("10" - 5);   // 5 ("10" converted to 10)
        console.log("10" * "2"); // 20 ("10" and "2" converted to numbers)
        console.log("hello" - 5); // NaN ("hello" converted to NaN)
        ```
      * **With `==`, `!=` (Loose Equality)**:
          * Attempts to convert operands to a common type before comparison. This can lead to unexpected results.
          * **Recommendation**: Always use strict equality (`===`) and strict inequality (`!==`) to avoid implicit coercion and ensure type and value comparison.
        <!-- end list -->
        ```javascript
        console.log(1 == "1");    // true (string "1" converted to number 1)
        console.log(0 == false);  // true (false converted to 0)
        console.log(null == undefined); // true (special case)
        console.log(0 == null);   // false
        ```

  * **Weird cases**:

      * `[] + {}` evaluates to `'[object Object]'`
          * The array `[]` is coerced to an empty string `""`.
          * The object `{}` is coerced to the string `"[object Object]"`.
          * Then, string concatenation occurs: `"" + "[object Object]"`.
      * `{} + []` evaluates to `0` (in some contexts, like browser console) or `'[object Object]'` (when explicitly treated as an expression).
          * When `{} + []` is at the beginning of a line in a browser console, `JS` might interpret `{}` as an empty code block, not an object literal. Then, `+[]` is interpreted as the unary plus operator applied to an empty array, which coerces `[]` to `0`.
          * When explicitly used as an expression (e.g., `console.log({} + [])`), it's treated as object concatenation, resulting in `"[object Object]"`. This context dependency makes it a "weird case."
      * `[] == false` evaluates to `true`
          * `[]` is coerced to an empty string `""`.
          * `false` is coerced to the number `0`.
          * Then `""` is coerced to `0` for comparison. So, `0 == 0` is `true`.
      * `'5' - 1` evaluates to `4`
          * The string `'5'` is implicitly coerced to the number `5` because the `-` operator only works with numbers.

-----

### 4\. Truthy / Falsy

In JavaScript, every value has an inherent boolean value when evaluated in a boolean context (e.g., in an `if` statement, a ternary operator, or with logical operators).

**Topics:**

  * **List of all falsy values**: These are the only values that evaluate to `false` in a boolean context. All other values are considered truthy.

    1.  `false` (the boolean primitive)
    2.  `0` (the number zero)
    3.  `-0` (the negative number zero)
    4.  `0n` (BigInt zero)
    5.  `""` (an empty string)
    6.  `null`
    7.  `undefined`
    8.  `NaN` (Not-a-Number)

  * **Use in conditions**: Falsy values are crucial for control flow.

    ```javascript
    let username = ""; // Falsy
    if (username) {
        console.log("Welcome, " + username);
    } else {
        console.log("Please enter your username."); // This will execute
    }

    let count = 0; // Falsy
    if (count) {
        console.log("Count is " + count);
    } else {
        console.log("Count is zero."); // This will execute
    }

    let data = null; // Falsy
    if (data) {
        console.log("Data exists.");
    } else {
        console.log("No data available."); // This will execute
    }
    ```

    All other values are **truthy**, including:

      * `true`
      * Any non-zero number (e.g., `1`, `-1`, `3.14`)
      * Any non-empty string (e.g., `"hello"`, `" "`)
      * Objects (e.g., `{}`, `[]`, `function() {}`) - **empty objects and arrays are truthy\!**
      * `Symbol()`
      * `BigInt` values other than `0n`

  * **Double negation `!!` to convert to boolean**: A common and concise idiom to explicitly convert any value to its strict boolean equivalent (`true` or `false`).

      * The first `!` converts the value to its boolean opposite.
      * The second `!` converts that boolean back to its opposite, effectively giving the original value's boolean representation.

    <!-- end list -->

    ```javascript
    console.log(!!0);         // false
    console.log(!!"");        // false
    console.log(!!null);      // false
    console.log(!!undefined); // false
    console.log(!!NaN);       // false
    console.log(!!1);         // true
    console.log(!!"hello");   // true
    console.log(!!{});        // true
    console.log(!![]);         // true
    ```

-----

### 5\. Short-Circuiting / Logical Operators

Logical operators (`||`, `&&`, `??`) in JavaScript exhibit "short-circuiting" behavior, meaning they don't always evaluate all operands. They return the value of one of the operands, not necessarily a boolean `true` or `false`.

**Topics:**

  * **`||` (Logical OR) evaluation**:

      * Evaluates operands from left to right.
      * Returns the **first truthy value** it encounters.
      * If all operands are falsy, it returns the **last operand**.

    <!-- end list -->

    ```javascript
    console.log(true || false);   // true
    console.log(false || true);   // true
    console.log(0 || 1);          // 1 (0 is falsy, 1 is truthy)
    console.log("" || "default"); // "default" ("" is falsy)
    console.log(null || undefined || "fallback"); // "fallback" (null and undefined are falsy)
    console.log(0 || false || null); // null (all falsy, returns the last one)
    ```

  * **`&&` (Logical AND) evaluation**:

      * Evaluates operands from left to right.
      * Returns the **first falsy value** it encounters.
      * If all operands are truthy, it returns the **last operand**.

    <!-- end list -->

    ```javascript
    console.log(true && false);   // false
    console.log(true && "hello"); // "hello" (true is truthy, returns "hello")
    console.log("hello" && 123);  // 123 ("hello" is truthy, returns 123)
    console.log(0 && "anything"); // 0 (0 is falsy, returns 0)
    console.log(null && "anything"); // null (null is falsy, returns null)
    ```

  * **`??` Nullish coalescing operator**:

      * Introduced in ES2020.
      * Returns the right-hand side operand when the left-hand side operand is `null` or `undefined`.
      * **Crucially, it does NOT treat `0` or `''` (empty string) as "nullish"**. This is the key difference from `||`.

    <!-- end list -->

    ```javascript
    let userSetting = null;
    let defaultSetting = "dark";
    console.log(userSetting ?? defaultSetting); // "dark" (userSetting is null)

    let count = 0;
    console.log(count ?? 100); // 0 (0 is not null or undefined)

    let emptyString = "";
    console.log(emptyString ?? "default text"); // "" (emptyString is not null or undefined)

    let value = undefined;
    console.log(value ?? "fallback"); // "fallback" (value is undefined)
    ```

  * **Practical use cases**:

      * **Default values**:
          * Using `||`: `const userName = inputName || 'Guest';` (If `inputName` is `null`, `undefined`, `""`, `0`, etc., `userName` will be `'Guest'`).
          * Using `??`: `const fontSize = userConfig.fontSize ?? 16;` (If `userConfig.fontSize` is `null` or `undefined`, `fontSize` will be `16`. If it's `0`, `fontSize` will be `0`).
      * **Conditional execution**:
          * `isAdmin && showAdminPanel();` (If `isAdmin` is `true`, `showAdminPanel()` will be called. If `isAdmin` is `false` or falsy, `showAdminPanel()` will not be called).
          * `const result = data && data.property;` (Safely access `data.property` only if `data` is not null/undefined/falsy).

-----

### 6\. Control Flow

Control flow statements dictate the order in which individual statements, instructions, or function calls are executed.

**Topics:**

  * **`if`, `else`, `else if`**: Execute different blocks of code based on whether a condition is `true` or `false`.

    ```javascript
    let temperature = 25;

    if (temperature > 30) {
        console.log("It's hot!");
    } else if (temperature > 20) {
        console.log("It's warm."); // This will execute
    } else {
        console.log("It's cold.");
    }
    ```

  * **`switch`**: Provides a more structured and often more readable alternative to a long chain of `else if` statements when you need to compare a single expression against multiple possible values.

      * The `break` keyword is crucial to exit the `switch` block once a match is found. Without `break`, execution will "fall through" to the next `case`.
      * The `default` case is optional and executes if no other `case` matches.

    <!-- end list -->

    ```javascript
    let day = "Monday";

    switch (day) {
        case "Monday":
            console.log("Start of the week.");
            break; // Exit switch
        case "Friday":
            console.log("End of the week.");
            break;
        default:
            console.log("Mid-week or weekend.");
    }
    ```

  * **Ternary Operator (`condition ? expr1 : expr2`)**: A concise, single-line shorthand for simple `if-else` statements.

      * If `condition` is `true`, `expr1` is evaluated and its result is returned.
      * If `condition` is `false`, `expr2` is evaluated and its result is returned.

    <!-- end list -->

    ```javascript
    let age = 18;
    let canVote = (age >= 18) ? "Yes, can vote" : "No, cannot vote";
    console.log(canVote); // "Yes, can vote"

    // Equivalent if-else:
    // let canVote;
    // if (age >= 18) {
    //     canVote = "Yes, can vote";
    // } else {
    //     canVote = "No, cannot vote";
    // }
    ```

  * **Nested and compound conditions**:

      * **Nested**: Placing one conditional statement inside another.
        ```javascript
        let loggedIn = true;
        let isAdmin = false;

        if (loggedIn) {
            if (isAdmin) {
                console.log("Welcome, Admin!");
            } else {
                console.log("Welcome, User!"); // This will execute
            }
        } else {
            console.log("Please log in.");
        }
        ```
      * **Compound**: Combining multiple conditions using logical operators (`&&` for AND, `||` for OR, `!` for NOT).
        ```javascript
        let score = 85;
        let attendance = 90;

        if (score >= 70 && attendance >= 80) {
            console.log("Passed the course."); // This will execute
        } else {
            console.log("Did not pass.");
        }

        let isWeekend = false;
        let isHoliday = true;

        if (isWeekend || isHoliday) {
            console.log("Enjoy your day off!"); // This will execute
        } else {
            console.log("Work day.");
        }
        ```

-----

### 7\. Loops

Loops are used to repeatedly execute a block of code until a specified condition is met.

**Topics:**

  * **`for`, `while`, `do...while`**

      * **`for` loop**: Best used when you know the number of iterations beforehand.
          * Syntax: `for (initialization; condition; increment/decrement) { // code }`
        <!-- end list -->
        ```javascript
        for (let i = 0; i < 5; i++) {
            console.log("For loop iteration: " + i); // 0, 1, 2, 3, 4
        }
        ```
      * **`while` loop**: Executes a block of code as long as a specified condition evaluates to `true`. The condition is checked *before* each iteration.
        ```javascript
        let count = 0;
        while (count < 3) {
            console.log("While loop iteration: " + count); // 0, 1, 2
            count++;
        }
        ```
      * **`do...while` loop**: Similar to `while`, but guarantees that the loop body will execute at least once, because the condition is checked *after* the first iteration.
        ```javascript
        let i = 0;
        do {
            console.log("Do-While loop iteration: " + i); // 0, 1, 2
            i++;
        } while (i < 3);

        let j = 5;
        do {
            console.log("Do-While executes once even if condition is false: " + j); // 5 (executes once)
            j++;
        } while (j < 3);
        ```

  * **Loop control: `break`, `continue`**

      * **`break`**: Terminates the current loop entirely and continues execution at the statement immediately following the loop.
        ```javascript
        for (let k = 0; k < 10; k++) {
            if (k === 5) {
                break; // Exit the loop when k is 5
            }
            console.log("Break example: " + k); // 0, 1, 2, 3, 4
        }
        ```
      * **`continue`**: Skips the current iteration of the loop and proceeds to the next one.
        ```javascript
        for (let m = 0; m < 5; m++) {
            if (m === 2) {
                continue; // Skip iteration when m is 2
            }
            console.log("Continue example: " + m); // 0, 1, 3, 4
        }
        ```

  * **`for...in` vs `for...of` (key vs value iteration)**

      * **`for...in`**: Iterates over **enumerable property names (keys)** of an object. It can also iterate over array indices, but this is generally **not recommended for arrays** because it can iterate over inherited properties and the order is not guaranteed.
        ```javascript
        const myObject = { a: 1, b: 2, c: 3 };
        for (const key in myObject) {
            // It's good practice to use hasOwnProperty to avoid iterating over inherited properties
            if (myObject.hasOwnProperty(key)) {
                console.log(`for...in: Key: ${key}, Value: ${myObject[key]}`);
            }
        }
        // Output:
        // for...in: Key: a, Value: 1
        // for...in: Key: b, Value: 2
        // for...in: Key: c, Value: 3

        const myArray = ["apple", "banana", "cherry"];
        for (const index in myArray) {
            console.log(`for...in (array): Index: ${index}, Value: ${myArray[index]}`);
        }
        // Output:
        // for...in (array): Index: 0, Value: apple
        // for...in (array): Index: 1, Value: banana
        // for...in (array): Index: 2, Value: cherry
        ```
      * **`for...of`**: Iterates over **values** of iterable objects (Arrays, Strings, Maps, Sets, NodeLists, etc.). This is the **preferred way to iterate over arrays and other iterables**.
        ```javascript
        const myArray = ["apple", "banana", "cherry"];
        for (const value of myArray) {
            console.log(`for...of (array): Value: ${value}`);
        }
        // Output:
        // for...of (array): Value: apple
        // for...of (array): Value: banana
        // for...of (array): Value: cherry

        const myString = "hello";
        for (const char of myString) {
            console.log(`for...of (string): Character: ${char}`);
        }
        // Output:
        // for...of (string): Character: h
        // for...of (string): Character: e
        // for...of (string): Character: l
        // for...of (string): Character: l
        // for...of (string): Character: o
        ```

  * **Looping over arrays, objects, strings**

      * **Arrays**:
          * `for` loop (by index): `for (let i = 0; i < arr.length; i++) { console.log(arr[i]); }`
          * `for...of` loop (by value): `for (const item of arr) { console.log(item); }` (Recommended)
          * `forEach()` method (see Array Operations): `arr.forEach(item => console.log(item));` (Recommended)
      * **Objects**:
          * `for...in` loop (by key, with `hasOwnProperty` check):
            ```javascript
            const user = { name: "Alice", age: 30 };
            for (const key in user) {
                if (user.hasOwnProperty(key)) {
                    console.log(`${key}: ${user[key]}`);
                }
            }
            ```
          * Using `Object.keys()`, `Object.values()`, `Object.entries()`: These methods return arrays that can then be iterated using `forEach` or `for...of`.
            ```javascript
            const user = { name: "Alice", age: 30 };
            Object.keys(user).forEach(key => console.log(key)); // "name", "age"
            Object.values(user).forEach(value => console.log(value)); // "Alice", 30
            Object.entries(user).forEach(([key, value]) => console.log(`${key}: ${value}`)); // "name: Alice", "age: 30"
            ```
      * **Strings**:
          * `for` loop (by index): `for (let i = 0; i < str.length; i++) { console.log(str[i]); }`
          * `for...of` loop (by character): `for (const char of str) { console.log(char); }` (Recommended for full Unicode support)

-----

### 8\. Functions

Functions are fundamental building blocks in JavaScript, allowing you to encapsulate reusable blocks of code. They are first-class citizens, meaning they can be treated like any other value (assigned to variables, passed as arguments, returned from other functions).

**Topics:**

  * **Declaration vs Expression**

      * **Function Declaration**: Defined using the `function` keyword, followed by a name, parameters, and a code block.
          * **Hoisted**: Can be called before their definition in the code.
        <!-- end list -->
        ```javascript
        greetDeclaration("Alice"); // "Hello, Alice!" (works due to hoisting)

        function greetDeclaration(name) {
            console.log(`Hello, ${name}!`);
        }
        ```
      * **Function Expression**: Defined by assigning an anonymous (or named) function to a variable.
          * **Not Hoisted**: Must be defined before they are called, similar to `let` and `const` variables.
        <!-- end list -->
        ```javascript
        // greetExpression("Bob"); // TypeError: greetExpression is not a function (not hoisted)

        const greetExpression = function(name) {
            console.log(`Hello, ${name}!`);
        };
        greetExpression("Bob"); // "Hello, Bob!"

        // Named Function Expression (name only accessible within the function)
        const factorial = function calculateFactorial(n) {
            if (n <= 1) return 1;
            return n * calculateFactorial(n - 1);
        };
        console.log(factorial(5)); // 120
        // console.log(calculateFactorial(3)); // ReferenceError: calculateFactorial is not defined
        ```

  * **Arrow Functions (`=>`)**

      * Introduced in ES6 (ES2015) as a more concise way to write functions.
      * **Concise Syntax**:
          * No `function` keyword.
          * Implicit `return` for single-expression bodies (no `{}` or `return` needed).
          * Parentheses around parameters are optional for a single parameter.
        <!-- end list -->
        ```javascript
        // Traditional function expression
        const addOld = function(a, b) {
            return a + b;
        };

        // Arrow function with multiple parameters, explicit return
        const add = (a, b) => {
            return a + b;
        };

        // Arrow function with single parameter, implicit return
        const square = num => num * num;

        // Arrow function with no parameters
        const sayHi = () => console.log("Hi!");
        ```
      * **`this` Binding (Lexical `this`)**: This is the most significant difference. Arrow functions **do not have their own `this` context**. Instead, they inherit `this` from the enclosing lexical (parent) scope at the time they are defined. This solves common `this` binding issues in traditional functions.
        ```javascript
        const person = {
            name: "Charlie",
            // Traditional function: 'this' depends on how it's called
            greetTraditional: function() {
                setTimeout(function() {
                    // console.log(this.name); // 'this' is window/undefined here
                    console.log("Traditional (needs bind/self): " + this.name);
                }, 100);
            },
            // Arrow function: 'this' is lexically bound to 'person' object
            greetArrow: function() {
                setTimeout(() => {
                    console.log("Arrow (lexical this): " + this.name); // 'this' refers to 'person'
                }, 100);
            }
        };
        person.greetTraditional(); // Output depends on strict mode (undefined or window.name)
        person.greetArrow();      // Output: Arrow (lexical this): Charlie
        ```
      * **Limitations**:
          * Cannot be used as constructors (`new` keyword).
          * Do not have their own `arguments` object (use rest parameters instead).
          * Cannot be used as method definitions in object literals if you need dynamic `this` (e.g., `this.propertyName`).

  * **Default Parameters**: Allow you to assign default values to function parameters if no value or `undefined` is passed for that argument.

    ```javascript
    function greet(name = "Guest", greeting = "Hello") {
        console.log(`${greeting}, ${name}!`);
    }
    greet("David");          // "Hello, David!"
    greet("Eve", "Hi");      // "Hi, Eve!"
    greet();                 // "Hello, Guest!"
    greet(undefined, "Hola"); // "Hola, Guest!"
    greet(null, "Hola");     // "Hola, null!" (null is a value, not undefined)
    ```

  * **Rest Parameters (`...rest`)**: Allows a function to accept an indefinite number of arguments as an array. It must be the last parameter in the function definition.

    ```javascript
    function sumAll(...numbers) {
        // numbers is an array [1, 2, 3, 4]
        return numbers.reduce((total, num) => total + num, 0);
    }
    console.log(sumAll(1, 2, 3, 4)); // 10

    function logDetails(name, age, ...hobbies) {
        console.log(`Name: ${name}, Age: ${age}`);
        console.log(`Hobbies: ${hobbies.join(", ")}`);
    }
    logDetails("Frank", 28, "reading", "hiking", "coding");
    // Output:
    // Name: Frank, Age: 28
    // Hobbies: reading, hiking, coding
    ```

  * **Spread Syntax in arguments (`...array`)**: The spread syntax expands an iterable (like an array or string) into individual elements. It's used when calling functions or creating new arrays/objects.

      * **When calling functions**: Spreads an array into individual arguments.
        ```javascript
        function multiply(a, b, c) {
            return a * b * c;
        }
        const nums = [2, 3, 4];
        console.log(multiply(...nums)); // 24 (equivalent to multiply(2, 3, 4))
        ```
      * **Creating new arrays/objects**: (See Array Operations for array examples)
        ```javascript
        const obj1 = { a: 1, b: 2 };
        const obj2 = { ...obj1, c: 3 }; // Creates a new object by copying properties of obj1
        console.log(obj2); // { a: 1, b: 2, c: 3 }
        ```

  * **Named vs anonymous functions**

      * **Named Functions**: Have an identifier (a name) after the `function` keyword.
          * **Benefits**: Easier to debug (name appears in stack traces), self-documenting, can be recursive.
        <!-- end list -->
        ```javascript
        function calculateArea(length, width) { // calculateArea is the name
            return length * width;
        }
        const myFunc = function namedExpression() { /* ... */ }; // namedExpression is the name
        ```
      * **Anonymous Functions**: Do not have an identifier. Often used as arguments to other functions (callbacks) or in IIFEs.
        ```javascript
        setTimeout(function() { // anonymous function as a callback
            console.log("Delayed message");
        }, 1000);

        const myArrowFunc = () => { /* ... */ }; // anonymous arrow function
        ```

  * **Callback functions**: A function passed as an argument to another function, to be executed later. This is a core concept in asynchronous JavaScript and event handling.

    ```javascript
    function fetchData(url, callback) {
        // Simulate fetching data
        setTimeout(() => {
            const data = `Data from ${url}`;
            callback(data); // Execute the callback with the fetched data
        }, 1000);
    }

    function processData(result) {
        console.log("Processing: " + result);
    }

    fetchData("api.example.com/users", processData); // processData is the callback
    // Output (after 1 second): Processing: Data from api.example.com/users
    ```

-----

### 9\. IIFE (Immediately Invoked Function Expressions)

An IIFE is a JavaScript function that runs as soon as it is defined. It's a design pattern that creates a private scope for variables, preventing them from polluting the global namespace.

**Topics:**

  * **Purpose**:

      * **Encapsulation/Private Scope**: Variables and functions declared inside an IIFE are not accessible from the outside, preventing naming conflicts with other scripts or the global environment. This is useful for creating modules or isolating code.
      * **Avoiding Global Pollution**: Especially important in older JavaScript codebases or when integrating third-party libraries that might introduce global variables.
      * **Module Pattern**: IIFEs were a common way to implement the module pattern before ES6 modules (`import`/`export`) became standard.
      * **Executing Code Once**: Ensures a block of code runs immediately and only once.

  * **Syntax**:

      * The most common syntax involves wrapping the function definition in parentheses `()` and then immediately invoking it with another set of parentheses `()`.
      * **Why the outer parentheses?**: The outer parentheses make the function a "function expression" rather than a "function declaration." A function declaration cannot be immediately invoked.
        ```javascript
        // Traditional IIFE syntax
        (function() {
            let privateVar = "I am private";
            console.log("IIFE executed!");
            // console.log(privateVar); // Accessible here
        })(); // Immediately invoked

        // privateVar; // ReferenceError: privateVar is not defined (not accessible outside)

        // Using arrow function for IIFE (ES6+)
        (() => {
            let anotherPrivateVar = "Also private";
            console.log("Arrow IIFE executed!");
        })();
        ```
      * **Variations**:
        ```javascript
        // Leading unary operators also make it an expression
        !function() { console.log("!"); }();
        +function() { console.log("+"); }();
        ```

-----

### 10\. Array Operations

Arrays are ordered, list-like objects in JavaScript. They come with a rich set of built-in methods for iteration, manipulation, and transformation.

**Topics:**

  * **Iteration (Non-mutating, return new values or perform actions)**

      * `forEach(callback)`: Executes a provided `callback` function once for each array element. It does not return a new array. Used for side effects (e.g., logging, updating DOM).
        ```javascript
        const numbers = [1, 2, 3];
        numbers.forEach((num, index) => {
            console.log(`forEach: Element at index ${index} is ${num}`);
        });
        // Output:
        // forEach: Element at index 0 is 1
        // forEach: Element at index 1 is 2
        // forEach: Element at index 2 is 3
        ```
      * `map(callback)`: Creates a **new array** populated with the results of calling a provided `callback` function on every element in the calling array.
        ```javascript
        const doubled = numbers.map(num => num * 2);
        console.log("map:", doubled); // [2, 4, 6]
        ```
      * `filter(callback)`: Creates a **new array** with all elements that pass the test implemented by the provided `callback` function.
        ```javascript
        const evens = numbers.filter(num => num % 2 === 0);
        console.log("filter:", evens); // [2]
        ```
      * `reduce(callback, initialValue)`: Executes a reducer `callback` function on each element of the array (from left to right), resulting in a single output value.
          * `callback` takes `accumulator`, `currentValue`, `currentIndex`, `array`.
          * `initialValue` is optional; if not provided, the first element is used as the initial accumulator.
        <!-- end list -->
        ```javascript
        const sum = numbers.reduce((acc, num) => acc + num, 0);
        console.log("reduce (sum):", sum); // 6

        const max = numbers.reduce((acc, num) => (num > acc ? num : acc), numbers[0]);
        console.log("reduce (max):", max); // 3
        ```
      * `find(callback)`: Returns the **value** of the first element in the array that satisfies the provided testing `callback` function. If no elements satisfy the test, `undefined` is returned.
        ```javascript
        const found = numbers.find(num => num > 1);
        console.log("find:", found); // 2
        ```
      * `some(callback)`: Checks if **at least one** element in the array satisfies the provided testing `callback` function. Returns `true` or `false`.
        ```javascript
        const hasEven = numbers.some(num => num % 2 === 0);
        console.log("some (has even):", hasEven); // true
        ```
      * `every(callback)`: Checks if **all** elements in the array satisfy the provided testing `callback` function. Returns `true` or `false`.
        ```javascript
        const allEven = numbers.every(num => num % 2 === 0);
        console.log("every (all even):", allEven); // false
        ```

  * **Mutating (Modifies the original array)**: These methods change the array in place.

      * `push(element1, ...)`: Adds one or more elements to the end of an array and returns the new `length`.
        ```javascript
        const fruits = ["apple", "banana"];
        fruits.push("cherry");
        console.log("push:", fruits); // ["apple", "banana", "cherry"]
        ```
      * `pop()`: Removes the last element from an array and returns that element.
        ```javascript
        const lastFruit = fruits.pop();
        console.log("pop:", fruits, lastFruit); // ["apple", "banana"], "cherry"
        ```
      * `shift()`: Removes the first element from an array and returns that element.
        ```javascript
        const firstFruit = fruits.shift();
        console.log("shift:", fruits, firstFruit); // ["banana"], "apple"
        ```
      * `unshift(element1, ...)`: Adds one or more elements to the beginning of an array and returns the new `length`.
        ```javascript
        fruits.unshift("grape", "kiwi");
        console.log("unshift:", fruits); // ["grape", "kiwi", "banana"]
        ```
      * `splice(start, deleteCount, item1, ...)`: A powerful method that changes the contents of an array by removing or replacing existing elements and/or adding new elements in place. Returns an array containing the deleted elements.
        ```javascript
        const colors = ["red", "green", "blue", "yellow"];
        colors.splice(1, 2, "purple", "orange"); // At index 1, delete 2 elements, then add "purple", "orange"
        console.log("splice (replace):", colors); // ["red", "purple", "orange", "yellow"]

        colors.splice(2, 0, "pink"); // At index 2, delete 0 elements, add "pink"
        console.log("splice (add):", colors); // ["red", "purple", "pink", "orange", "yellow"]

        const removed = colors.splice(0, 1); // At index 0, delete 1 element
        console.log("splice (remove):", colors, removed); // ["purple", "pink", "orange", "yellow"], ["red"]
        ```
      * `sort(compareFunction)`: Sorts the elements of an array in place and returns the sorted array. By default, it sorts elements as strings. For numbers, you need a `compareFunction`.
        ```javascript
        const unsortedNums = [3, 1, 4, 1, 5, 9];
        unsortedNums.sort((a, b) => a - b); // Ascending numeric sort
        console.log("sort (numeric):", unsortedNums); // [1, 1, 3, 4, 5, 9]

        const unsortedStrings = ["banana", "apple", "cherry"];
        unsortedStrings.sort(); // Lexicographical sort
        console.log("sort (string):", unsortedStrings); // ["apple", "banana", "cherry"]
        ```
      * `reverse()`: Reverses the order of the elements in an array in place.
        ```javascript
        const arrToReverse = [1, 2, 3];
        arrToReverse.reverse();
        console.log("reverse:", arrToReverse); // [3, 2, 1]
        ```

  * **Non-mutating (Returns a new array)**: These methods create a new array without altering the original.

      * `slice(start, end)`: Returns a shallow copy of a portion of an array into a new array object selected from `start` to `end` (end not included).
        ```javascript
        const original = [1, 2, 3, 4, 5];
        const sliced = original.slice(1, 4); // Elements from index 1 up to (but not including) 4
        console.log("slice:", sliced);     // [2, 3, 4]
        console.log("original after slice:", original); // [1, 2, 3, 4, 5] (unchanged)
        ```
      * `concat(array1, array2, ...)`: Used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.
        ```javascript
        const arr1 = [1, 2];
        const arr2 = [3, 4];
        const combinedSpread = [...arr1, ...arr2]; // Often preferred over concat()
        console.log("concat:", combinedSpread); // [1, 2, 3, 4]
        ```
      * `join(separator)`: Joins all elements of an array into a string. The `separator` (defaulting to a comma) is placed between each element.
        ```javascript
        const words = ["Hello", "World"];
        console.log("join (space):", words.join(" ")); // "Hello World"
        console.log("join (comma):", words.join());    // "Hello,World"
        ```

  * **Array destructuring**: A convenient syntax that allows you to unpack values from arrays (or properties from objects) into distinct variables.

    ```javascript
    const coordinates = [10, 20, 30];
    const [x, y, z] = coordinates;
    console.log(`Destructuring: x=${x}, y=${y}, z=${z}`); // x=10, y=20, z=30

    // Skipping elements
    const [first, , third] = ["a", "b", "c"];
    console.log(`Skipping: ${first}, ${third}`); // a, c

    // With rest parameter for remaining elements
    const [head, ...tail] = [1, 2, 3, 4];
    console.log(`Head: ${head}, Tail: ${tail}`); // Head: 1, Tail: 2,3,4
    ```

  * **Flattening arrays: `flat()`**

      * `flat(depth)`: Creates a new array with all sub-array elements concatenated into it recursively up to a specified `depth`. The `depth` defaults to 1.
        ```javascript
        const nestedArray = [1, [2, 3], [4, [5, 6]]];
        console.log("flat (default):", nestedArray.flat());     // [1, 2, 3, 4, [5, 6]]
        console.log("flat (depth 2):", nestedArray.flat(2));    // [1, 2, 3, 4, 5, 6]
        console.log("flat (Infinity):", nestedArray.flat(Infinity)); // [1, 2, 3, 4, 5, 6] (flattens all levels)
        ```
      * `flatMap(callback)`: Introduced in ES2019. It's a combination of `map()` followed by `flat()` with a depth of 1. It first maps each element using a mapping function, then flattens the result into a new array.
        ```javascript
        const words = ["Hello World", "JavaScript is fun"];
        const chars = words.flatMap(sentence => sentence.split(" "));
        console.log("flatMap:", chars); // ["Hello", "World", "JavaScript", "is", "fun"]
        ```

  * **Spread operator (`...`) in arrays**: The spread syntax can be used to expand an array into individual elements.

      * **Creating a shallow copy**: Creates a new array with the same elements.
        ```javascript
        const originalArray = [1, 2, 3];
        const copyArray = [...originalArray];
        console.log("Spread copy:", copyArray); // [1, 2, 3]
        console.log(originalArray === copyArray); // false (different array objects)
        ```
      * **Concatenating arrays**: A concise alternative to `concat()`.
        ```javascript
        const arrA = [1, 2];
        const arrB = [3, 4];
        const combinedSpread = [...arrA, ...arrB];
        console.log("Spread concat:", combinedSpread); // [1, 2, 3, 4]
        ```
      * **Adding elements to an array**:
        ```javascript
        const baseItems = ["milk", "bread"];
        const shoppingList = [...baseItems, "eggs", "cheese"];
        console.log("Spread add:", shoppingList); // ["milk", "bread", "eggs", "cheese"]
        ```

-----

### 11\. Strings and String Operations

Strings are a fundamental data type in JavaScript for representing text. They are immutable primitive values, meaning once a string is created, its content cannot be changed. Any string operation that appears to modify a string actually returns a *new* string.

**Topics:**

  * **String Immutability**:

      * Strings are primitive values, and their content cannot be altered after creation.
      * Methods that "modify" strings (like `toUpperCase()`, `replace()`) always return a *new string*. The original string remains unchanged.

    <!-- end list -->

    ```javascript
    let originalString = "Hello";
    let modifiedString = originalString.toUpperCase();
    console.log("Original:", originalString); // "Hello"
    console.log("Modified:", modifiedString); // "HELLO"
    ```

  * **Accessing Characters**:

      * **Bracket Notation (`[]`)**: Accesses individual characters by their zero-based index. Returns `undefined` for out-of-bounds indices.
        ```javascript
        const str = "JavaScript";
        console.log(str[0]); // "J"
        console.log(str[4]); // "S"
        console.log(str[100]); // undefined
        ```
      * **`charAt(index)`**: Returns the character at the specified index. Returns an empty string `""` for out-of-bounds indices.
        ```javascript
        console.log(str.charAt(0)); // "J"
        console.log(str.charAt(4)); // "S"
        console.log(str.charAt(100)); // ""
        ```

  * **String Length**:

      * `.length`: A property (not a method) that returns the number of characters in the string.
        ```javascript
        const myString = "Web Development";
        console.log("Length:", myString.length); // 15
        ```

  * **Case Conversion**:

      * `toLowerCase()`: Returns a new string with all characters converted to lowercase.
      * `toUpperCase()`: Returns a new string with all characters converted to uppercase.
        ```javascript
        let text = "Hello World";
        console.log(text.toLowerCase()); // "hello world"
        console.log(text.toUpperCase()); // "HELLO WORLD"
        ```

  * **Searching Strings**:

      * `indexOf(substring, fromIndex)`: Returns the index of the first occurrence of a specified `substring`. Returns `-1` if not found. `fromIndex` is optional.
      * `lastIndexOf(substring, fromIndex)`: Returns the index of the last occurrence of a specified `substring`. Returns `-1` if not found. `fromIndex` is optional.
        ```javascript
        let sentence = "The quick brown fox jumps over the lazy dog.";
        console.log(sentence.indexOf("fox"));    // 16
        console.log(sentence.lastIndexOf("the")); // 31
        console.log(sentence.indexOf("cat"));    // -1
        ```
      * `includes(substring, position)`: Returns `true` if the string contains the specified `substring`, `false` otherwise. `position` is optional.
        ```javascript
        console.log(sentence.includes("quick")); // true
        console.log(sentence.includes("rabbit")); // false
        ```
      * `startsWith(prefix, position)`: Returns `true` if the string starts with the specified `prefix`. `position` is optional.
      * `endsWith(suffix, length)`: Returns `true` if the string ends with the specified `suffix`. `length` is optional.
        ```javascript
        console.log(sentence.startsWith("The")); // true
        console.log(sentence.endsWith("dog."));  // true
        console.log(sentence.startsWith("quick", 4)); // true (starts with 'quick' from index 4)
        ```

  * **Extracting Parts of a String**: These methods return a new string containing the extracted part.

      * `slice(startIndex, endIndex)`: Extracts a section of a string and returns it as a new string.
          * `startIndex`: The index at which to begin extraction (inclusive).
          * `endIndex`: The index at which to end extraction (exclusive). If omitted, extracts to the end of the string.
          * Supports negative indices (counts from the end of the string).
        <!-- end list -->
        ```javascript
        let data = "apple,banana,cherry";
        console.log(data.slice(6, 12));  // "banana"
        console.log(data.slice(6));      // "banana,cherry"
        console.log(data.slice(-6));     // "cherry"
        ```
      * `substring(startIndex, endIndex)`: Similar to `slice()`, but does **not accept negative indices**. If `startIndex` is greater than `endIndex`, it swaps the arguments.
        ```javascript
        console.log(data.substring(6, 12));  // "banana"
        console.log(data.substring(12, 6));  // "banana" (swaps arguments)
        ```
      * `substr(startIndex, length)`: Deprecated. Extracts `length` characters from `startIndex`.
        ```javascript
        // console.log(data.substr(6, 6)); // "banana"
        ```

  * **String Manipulation**:

      * `concat(string1, string2, ...)`: Joins two or more strings and returns a new string. Often replaced by `+` operator or template literals.
        ```javascript
        let s1 = "Hello";
        let s2 = "World";
        console.log(s1.concat(" ", s2)); // "Hello World"
        console.log(`${s1} ${s2}`);      // "Hello World" (preferred)
        ```
      * `trim()`: Removes whitespace from both ends of a string.
      * `trimStart()` (or `trimLeft()`): Removes whitespace from the beginning of a string.
      * `trimEnd()` (or `trimRight()`): Removes whitespace from the end of a string.
        ```javascript
        let padded = "   Trim Me   ";
        console.log(`"${padded.trim()}"`);       // "Trim Me"
        console.log(`"${padded.trimStart()}"`); // "Trim Me   "
        ```
      * `replace(searchValue, replaceValue)`: Searches a string for a specified value or a regular expression, and returns a new string where the first match is replaced.
          * For global replacement, use `replaceAll()` or a regular expression with the `g` flag.
        <!-- end list -->
        ```javascript
        let strReplace = "Dog, Cat, Dog";
        console.log(strReplace.replace("Dog", "Bird")); // "Bird, Cat, Dog" (only first occurrence)
        ```
      * `replaceAll(searchValue, replaceValue)`: Returns a new string with all occurrences of `searchValue` replaced with `replaceValue`.
        ```javascript
        console.log(strReplace.replaceAll("Dog", "Bird")); // "Bird, Cat, Bird"
        ```
      * `split(separator, limit)`: Divides a string into an ordered list of substrings (an array) by searching for the `separator`.
        ```javascript
        let csv = "apple,banana,cherry";
        console.log(csv.split(","));     // ["apple", "banana", "cherry"]
        console.log(csv.split("a"));     // ["", "pple,", "nana,cherry"]
        console.log("Hello".split(""));  // ["H", "e", "l", "l", "o"]
        ```
      * `repeat(count)`: Returns a new string consisting of the object on which it was called, concatenated `count` times.
        ```javascript
        console.log("abc".repeat(3)); // "abcabcabc"
        ```

  * **Template Literals (`` ` ``)**:

      * Already covered in Data Types, but important to reiterate their utility for string operations.
      * Allow for embedded expressions (`${expression}`).
      * Support multi-line strings without explicit escape characters (`\n`).

    <!-- end list -->

    ```javascript
    const product = "Laptop";
    const price = 1200;
    const description = `The ${product} costs $${price}.
    It's a great deal!`;
    console.log(description);
    // Output:
    // The Laptop costs $1200.
    // It's a great deal!
    ```

-----

### 12\. Strict Mode

Strict mode (`'use strict'`) is a way to opt in to a restricted variant of JavaScript. It helps write "secure" JavaScript by eliminating some silent errors, fixing mistakes that make it difficult for JavaScript engines to perform optimizations, and prohibiting some syntax likely to be defined in future versions of ECMAScript.

**Topics:**

  * **What is `'use strict'`?**

      * A literal string expression (`'use strict'` or `"use strict"`) placed at the beginning of a script or a function.
      * It's not a statement but a directive.

  * **Benefits**:

    1.  **Catches Common Coding Errors**: Turns some JavaScript "silent errors" into thrown errors (e.g., assigning to a non-writable property, deleting an undeletable property).
    2.  **Prevents Implicit Globals**: Variables assigned without declaration (e.g., `x = 10;`) will throw a `ReferenceError` instead of creating a global variable. This is a significant improvement for preventing accidental global pollution.
        ```javascript
        // Without 'use strict':
        function sloppyFunction() {
            undeclaredVar = "I'm global!"; // Creates a global variable
        }
        sloppyFunction();
        console.log(undeclaredVar); // "I'm global!"

        // With 'use strict':
        function strictFunction() {
            'use strict';
            // undeclaredVar = "I'm global!"; // ReferenceError: undeclaredVar is not defined
        }
        // strictFunction();
        ```
    3.  **Simplifies `this` Context**: In non-strict mode, `this` inside a function called without an explicit context (e.g., `myFunction()`) defaults to the global object (`window` in browsers). In strict mode, `this` will be `undefined` in such cases, preventing accidental global object modification.
        ```javascript
        // Without 'use strict':
        function showThisNonStrict() {
            console.log(this); // In browser, typically 'Window' object
        }
        showThisNonStrict();

        // With 'use strict':
        function showThisStrict() {
            'use strict';
            console.log(this); // undefined
        }
        showThisStrict();
        ```
    4.  **Disallows Some Unsafe/Confusing Features**:
          * Disables `with` statement.
          * Disallows `delete` on plain names (variables, functions).
          * Disallows duplicate parameter names in functions.
          * Makes `eval` safer by preventing it from introducing new variables into the surrounding scope.

  * **How to apply**:

      * **Globally**: Place `'use strict';` at the very beginning of your JavaScript file. This applies strict mode to the entire script.
        ```javascript
        // my_script.js
        'use strict';
        // All code below here is in strict mode
        let x = 10;
        // y = 20; // ReferenceError
        ```
      * **Within a function**: Place `'use strict';` at the beginning of a function body. This applies strict mode only to that specific function and its nested functions.
        ```javascript
        function strictModeFunction() {
            'use strict';
            // Code inside this function is in strict mode
            let a = 1;
            // b = 2; // ReferenceError
        }

        function normalModeFunction() {
            // Code here is not in strict mode
            c = 3; // Creates global variable (if not in a strict script)
        }
        ```
      * **Recommendation**: It is highly recommended to use strict mode, especially for new codebases, to write more robust and maintainable JavaScript. Modern JavaScript modules (ESM) are automatically in strict mode, so you don't need to declare it explicitly.

-----

