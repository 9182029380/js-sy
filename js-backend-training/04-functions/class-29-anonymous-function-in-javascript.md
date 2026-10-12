# Class 29: Anonymous Function in JavaScript

## 1. Definition
An **anonymous function** is a function **without a name**. It is usually created inline and assigned to a variable, passed as an argument or run immediately.

## 2. Usage
- Callbacks: `setTimeout(function () { ... }, 1000)`.
- Array methods: `arr.map(function (x) { return x * 2; })`.
- Event handlers and route handlers.
- IIFE (Immediately Invoked Function Expression) to create a private scope.
- Short arrow functions in modern code.

## 3. Description
Forms:
```js
function () { ... }          // anonymous function expression
() => { ... }                // anonymous arrow function
(function () { ... })();     // IIFE
```
- Cannot be a function declaration (declarations need a name).
- When assigned to a variable, modern engines **infer the name** (`const f = function(){}` gets `f.name === "f"`).
- **Drawbacks**: harder to read in stack traces and cannot call itself by name. A **named function expression** (`function fact(n) {...}`) fixes this.
- Anonymous arrow functions inherit `this` from the surrounding scope.

## 4. Examples

### Example 1: Anonymous function in a variable
```js
const hello = function () {
  return "Hello!";
};
console.log(hello());      // Hello!
console.log(hello.name);   // hello (inferred)
```

### Example 2: As a callback
```js
const prices = [100, 250, 400];
const withTax = prices.map(function (p) {
  return p * 1.18;
});
console.log(withTax);

const doubled = prices.map((p) => p * 2);   // arrow version
console.log(doubled);

setTimeout(function () {
  console.log("Runs after 500 ms");
}, 500);
```

### Example 3: IIFE and a named function expression
```js
(function () {
  const secret = "hidden";
  console.log("IIFE ran, secret is", secret);
})();
// console.log(secret);   // ReferenceError (private scope)

const factorial = function fact(n) {
  return n <= 1 ? 1 : n * fact(n - 1);   // can call itself by name
};
console.log(factorial(5));   // 120
```

## 5. Assignments
1. Use an anonymous function with `filter` to keep only the even numbers from `[1,2,3,4,5,6]`.
2. Write an IIFE that initialises a counter variable privately and prints a start message.
3. Rewrite three anonymous `function` callbacks as arrow functions.
4. Create a recursive function using a named function expression to compute the sum of numbers from 1 to n.

## 6. MCQs
**Q1.** An anonymous function is:
- A) A function that returns nothing
- B) A function without a name
- C) A function that cannot be called
- D) A built-in function

**Q2.** What does an IIFE do?
- A) Runs when the page loads
- B) Is defined and runs immediately
- C) Creates a class
- D) Is hoisted

**Q3.** Which is an anonymous function?
- A) `function add() {}`
- B) `const add = function () {};` (the function itself has no name)
- C) `class A {}`
- D) `function* gen() {}`

**Q4.** Why use a named function expression?
- A) Faster execution
- B) Easier debugging and recursion
- C) To create globals
- D) To enable hoisting

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **B**. The function expression is anonymous even though the variable has a name.
- Q4: **B**.
