
## JS Revision STRUCTURE

---

### 🔹 1. **Variables & Declarations**

**Topics:**

* `var`, `let`, `const` — redeclaration, reassignment, scoping
* Block Scope vs Function Scope
* Default values and declaration rules
* Variable Naming Best Practices
* Global variables and implicit globals (missing earlier ✅ now included)


---

### 🔹 2. **Data Types**

**Topics:**

* Primitive Types: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`
* Reference Types: `object`, `array`, `function`
* `typeof` quirks (`typeof null === 'object'`)
* Copy by value vs copy by reference



---

### 🔹 3. **Type Conversion & Coercion**

**Topics:**

* Explicit Conversion (`String()`, `Number()`, `Boolean()`)
* Implicit Coercion (with `+`, `-`, `==`, `!=`)
* Weird cases: `[] + {}`, `[] == false`, `'5' - 1`



---

### 🔹 4. **Truthy / Falsy**

**Topics:**

* List of all falsy values
* Use in conditions
* Double negation `!!` to convert to boolean



---

### 🔹 5. **Short-Circuiting / Logical Ops**

**Topics:**

* `||`, `&&` evaluation
* `??` Nullish coalescing operator
* Practical use cases: default values, conditionals



---

### 🔹 6. **Control Flow**

**Topics:**

* `if`, `else`, `else if`
* `switch`
* Ternary Operator
* Nested and compound conditions


---

### 🔹 7. **Loops**

**Topics:**

* `for`, `while`, `do...while`
* Loop control: `break`, `continue`
* `for...in` vs `for...of` (key vs value iteration)
* Looping over arrays, objects, strings



---

### 🔹 8. **Functions**

**Topics:**

* Declaration vs Expression
* Arrow Functions (and `this` binding)
* Default Parameters
* Rest Parameters
* Spread syntax in arguments
* Named vs anonymous functions
* Callback functions



---

### 🔹 9. **IIFE (Immediately Invoked Function Expressions)**

**Included** — No missing points

---

### 🔹 10. **Array Operations**

**Topics:**

* Iteration: `forEach`, `map`, `filter`, `reduce`, `find`, `some`, `every`
* Mutating: `push`, `pop`, `shift`, `unshift`, `splice`, `sort`, `reverse`
* Non-mutating: `slice`, `concat`, `join`
* Array destructuring
* Flattening arrays: `flat()`
* Spread operator in arrays


---

### 🔹 11. **Objects**

**Topics:**

* Dot vs Bracket notation
* Adding/removing properties
* Nested access + optional chaining
* Looping: `for...in`, `Object.keys`, `entries`, `values`
* Object merging: `Object.assign`, spread
* Object destructuring
* Freezing, sealing objects (❗was missing earlier ✅ now included)
* `in` operator


---

### 🔹 12. **Hoisting**

**Topics:**

* Variable Hoisting: `var` is hoisted, `let/const` not accessible (TDZ)
* Function Hoisting: Declarations hoisted, expressions not
* Temporal Dead Zone (TDZ)
* Illegal shadowing (❗was missing ✅ now included)


---

### 🔹 13. **Scope**

**Topics:**

* Global, Function, Block scope
* Lexical scope
* Shadowing (especially illegal shadowing with `let` and `var`)
* Scope Chain



---

### 🔹 14. **Closures**

**Topics:**

* Definition and how lexical environment preserves access
* Common examples: counter, private variables
* Closure inside loops with `var` and `setTimeout`
* Use in factories/memoization


---

### 🔹 15. **The `this` Keyword**

**Topics:**

* Global context
* Inside regular functions (strict vs non-strict)
* In objects
* Arrow functions (lexical `this`)
* Inside event handlers
* In classes
* `call`, `apply`, `bind`



---

### 🔹 16. **Execution Context & Call Stack**

**Topics:**

* Global, Functional, Eval execution context
* Memory creation + execution phase
* Call stack behavior
* Scope chaining



---

### 🔹 17. **Asynchronous JS**

**Topics:**

* Callbacks
* Promises (`then`, `catch`, `finally`)
* Async/await
* Error handling in async code
* Real-world fetch examples



---

### 🔹 18. **Event Loop**

**Topics:**

* Call Stack
* Web APIs
* Callback Queue
* Microtask Queue (Promises)
* Event Loop working
* Execution order: `setTimeout`, `Promise.resolve`, `queueMicrotask`
* Real example walkthrough



---

### 🔹 19. **DOM Basics**

**Topics:**

* `getElementById`, `querySelector`, `classList`
* `innerText` vs `innerHTML`
* `addEventListener`
* Creating/removing elements
* DOM traversal



---

### 🔹 20. **ES6+ Enhancements**

**Topics:**

* `let`, `const`
* Arrow Functions
* Template Literals
* Destructuring (Array/Object)
* Spread/Rest
* Default parameters
* `for...of`, `Object.entries`
* Modules (`import`, `export`)
* Optional chaining `?.`
* Nullish coalescing `??`



---

### 🔹 21. **Object-Oriented JS**

**Topics:**

* Constructor Functions
* Prototypes & Inheritance
* Prototype Chain
* `__proto__`, `Object.create`
* ES6 Classes
* `constructor`, `extends`, `super`
* Static methods



---

### 🔹 22. **Error Handling**

**Topics:**

* `try...catch...finally`
* `throw` custom errors
* Async errors with `try/catch`
* Re-throwing errors



---

### 🔹 23. **Advanced Concepts**

**Topics:**

* Debouncing
* Throttling
* Memoization
* Currying
* Event Delegation
* Polyfills (`map`, `filter`, `reduce`)
* Deep Copying: `structuredClone()`, `JSON.parse`, lodash
* Garbage Collection (basic)

