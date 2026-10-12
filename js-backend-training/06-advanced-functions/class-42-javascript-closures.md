# Class 42: JavaScript Closures

## 1. Definition
A **closure** is a function that **remembers the variables of the scope where it was created**, even after that outer scope has finished running.

## 2. Usage
- **Private state** (counters, caches, tokens) that outside code cannot touch.
- **Function factories** (`makeMultiplier(3)`, `createLogger("auth")`).
- **Callbacks and event handlers** that need access to earlier values.
- Memoization, debounce/throttle, once-only functions and module patterns.
- Middleware configuration in Express-style frameworks.

## 3. Description
- Every function has access to: its own variables, its parent's variables and globals (this chain is the **lexical scope**).
- When an inner function is returned or passed elsewhere, it **keeps a live link** to the outer variables.
- The outer variables are **not copied**: the closure sees later changes too.
- Each call to the outer function creates a **new, separate** set of variables.
- **Benefits**: data privacy, state without globals, partial application.
- **Cost**: variables captured by a closure stay in memory as long as the closure exists. Release references you no longer need to avoid memory leaks.
- Classic loop trap: `var` in loops shares one variable. `let` creates one per iteration.

## 4. Examples

### Example 1: Counter with private state
```js
function createCounter() {
  let count = 0;                 // private
  return {
    increment() { count++; return count; },
    reset() { count = 0; }
  };
}
const a = createCounter();
const b = createCounter();
console.log(a.increment(), a.increment());   // 1 2
console.log(b.increment());                  // 1 (separate state)
// console.log(count);                       // ReferenceError
```

### Example 2: Function factory
```js
function multiplier(factor) {
  return (n) => n * factor;
}
const double = multiplier(2);
const triple = multiplier(3);
console.log(double(5), triple(5));   // 10 15

function logger(prefix) {
  return (msg) => console.log(`[${prefix}] ${msg}`);
}
const authLog = logger("AUTH");
authLog("User signed in");
```

### Example 3: Once and memoize, plus the loop trap
```js
function once(fn) {
  let called = false, result;
  return (...args) => {
    if (!called) { called = true; result = fn(...args); }
    return result;
  };
}
const init = once(() => { console.log("Initialising..."); return 42; });
console.log(init(), init());   // logs once, then 42 42

function memoize(fn) {
  const cache = new Map();
  return (n) => cache.has(n) ? cache.get(n) : (cache.set(n, fn(n)), cache.get(n));
}
const slowSquare = (n) => { console.log("computing", n); return n * n; };
const fastSquare = memoize(slowSquare);
console.log(fastSquare(9), fastSquare(9));   // computes once

for (var i = 0; i < 3; i++) setTimeout(() => console.log("var", i), 0);   // 3 3 3
for (let j = 0; j < 3; j++) setTimeout(() => console.log("let", j), 0);   // 0 1 2
```

## 5. Assignments
1. Create a `bankAccount(initial)` closure with `deposit`, `withdraw` and `getBalance`, where the balance cannot be changed directly. Prevent overdraft.
2. Write `createIdGenerator(prefix)` that returns a function producing `USR-1`, `USR-2`, ...
3. Write a `rateLimiter(maxCalls)` closure that allows only `maxCalls` calls and then returns `"Limit reached"`.
4. Fix the `var` loop with `setTimeout` using a closure (IIFE) and again using `let`. Explain why both work.

## 6. MCQs
**Q1.** A closure is:
- A) A function that has no variables
- B) A function that remembers its outer scope variables
- C) A function that cannot be called
- D) A function inside a class

**Q2.** Each call to `createCounter()` produces:
- A) The same shared `count`
- B) A new independent `count`
- C) A global `count`
- D) An error

**Q3.** Which is a common use of closures?
- A) Creating private state
- B) Declaring global constants
- C) Importing modules
- D) Sorting arrays

**Q4.** What does this print? `for (var i=0;i<3;i++) setTimeout(()=>console.log(i),0);`
- A) 0 1 2
- B) 3 3 3
- C) 1 2 3
- D) 0 0 0

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **A**.
- Q4: **B**.
