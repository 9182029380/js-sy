# Class 02: Features of JavaScript

## 1. Definition
The **features of JavaScript** are the core characteristics that define how the language behaves: how it is executed, how it handles types, functions, objects and asynchronous work.

## 2. Usage
Knowing these features helps you understand why JS code behaves the way it does, especially in backend work: why a server can handle thousands of requests with one thread, why functions can be passed as arguments (callbacks, middleware), and why type bugs appear at runtime.

## 3. Description
| Feature | Meaning |
|---|---|
| Interpreted / JIT compiled | No separate compile step by the developer. The engine compiles code on the fly. |
| Dynamically typed | Types are checked at runtime. Variables are not tied to a type. |
| Lightweight and fast | Small runtime, V8 optimises hot code. |
| Prototype-based OOP | Objects inherit from other objects. `class` syntax is built on prototypes. |
| First-class functions | Functions are values. They can be stored, passed and returned. |
| Single-threaded, event-driven | One call stack plus an event loop for non-blocking I/O. |
| Asynchronous | Callbacks, Promises and `async/await` handle waiting work. |
| Cross-platform | Same code runs on Windows, Linux, macOS, browsers and servers. |
| JSON support | JSON comes from JS object syntax, so API data is natural to handle. |
| Rich ecosystem | npm is among the largest package registries in the world. |

## 4. Examples

### Example 1: Functions are first-class
```js
function square(n) { return n * n; }

const op = square;                 // stored in a variable
function apply(fn, value) { return fn(value); }  // passed as an argument
console.log(apply(op, 6));         // 36
```

### Example 2: Dynamic typing and loose behaviour
```js
let x = "5";
console.log(x * 2);   // 10  (string converted to number)
console.log(x + 2);   // "52" (number converted to string)
```
This flexibility is powerful but a common source of bugs. Always know your types.

### Example 3: Non-blocking asynchronous behaviour
```js
console.log("1. Start");
setTimeout(() => console.log("3. Finished waiting"), 1000);
console.log("2. Continue immediately");
```
**Output order**: `1. Start`, `2. Continue immediately`, `3. Finished waiting`. The timer does not block the code below it. A Node server works the same way while waiting for a database.

## 5. Assignments
1. Write a table in your own words listing five JavaScript features with one real backend benefit for each.
2. Create a function `shout(text)` returning uppercase text. Store it in a variable `fn`, then pass it to another function `repeat(fn, text, times)` that calls it `times` times.
3. Predict, then run, the output of `"10" - 2`, `"10" + 2`, `"abc" * 2`. Explain each result.
4. Write code using `setTimeout` that prints `A`, `B`, `C` in the order `A`, `C`, `B` without using any delay for `A` and `C`.

## 6. MCQs
**Q1.** JavaScript is best described as:
- A) Statically typed and compiled
- B) Dynamically typed and JIT-compiled by the engine
- C) Only for browsers
- D) Class-based only

**Q2.** What does "first-class function" mean?
- A) A function that runs first
- B) A function treated like any other value
- C) A function with no parameters
- D) A built-in function

**Q3.** What is the output of `console.log("5" + 3)`?
- A) 8
- B) `"53"`
- C) NaN
- D) Error

**Q4.** Why can Node.js serve many requests with a single thread?
- A) It creates a new thread per request
- B) It uses an event loop and non-blocking I/O
- C) It runs multiple JVMs
- D) It disables the call stack

### Answer Key
- Q1: **B**.
- Q2: **B**. Functions can be stored, passed and returned like values.
- Q3: **B**. `+` with a string concatenates, giving `"53"`.
- Q4: **B**. I/O waiting is handed off, the event loop continues with other work.
