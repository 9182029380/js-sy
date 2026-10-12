# Class 12: JavaScript var

## 1. Definition
`var` is the original JavaScript keyword for declaring variables (since ES1). A `var` variable is **function scoped** (or global if declared outside functions) and is **hoisted** to the top of its scope with the value `undefined`.

## 2. Usage
- Reading and maintaining **legacy code** (ES5 and older libraries).
- Understanding interview questions about hoisting and scope.
- In new code, prefer `let` and `const`.

## 3. Description
- **Function scope**: visible in the whole function, ignoring `if`/`for` blocks.
- **Hoisting**: the declaration moves to the top of the scope, but the assignment stays where it is. Reading before assignment gives `undefined`, not an error.
- **Re-declaration allowed**: `var a = 1; var a = 2;` is legal.
- **Re-assignment allowed**.
- **Global `var`** becomes a property of `window` in browsers (not in Node modules).
- **Loop closure problem**: one shared `var i` across iterations.

## 4. Examples

### Example 1: Function scope ignores blocks
```js
function test() {
  if (true) {
    var message = "inside if";
  }
  console.log(message);   // inside if (leaked out of the block)
}
test();
```

### Example 2: Hoisting and re-declaration
```js
console.log(count);   // undefined (hoisted, not assigned yet)
var count = 5;
var count = 10;       // allowed
console.log(count);   // 10
```

### Example 3: The classic loop problem
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
// prints 3, 3, 3  (all callbacks share one i)
```
With `let` instead of `var`, this prints `0, 1, 2`.

## 5. Assignments
1. Write a function using `var` inside an `if` block and prove the variable is visible outside the block. Explain why.
2. Predict the output of a script that logs a `var` variable before and after it is assigned. Run to verify.
3. Fix the loop closure example so it prints `0 1 2`, once with `let` and once with an IIFE (function that runs immediately) using `var`.
4. Re-declare the same `var` twice, then try the same with `let`. Record the difference in errors.

## 6. MCQs
**Q1.** The scope of `var` is:
- A) Block
- B) Function (or global)
- C) Module only
- D) Statement

**Q2.** What does this print? `console.log(a); var a = 3;`
- A) 3
- B) `ReferenceError`
- C) `undefined`
- D) `null`

**Q3.** Can `var x` be redeclared in the same scope?
- A) Yes
- B) No
- C) Only in strict mode
- D) Only inside functions

**Q4.** In `for (var i = 0; i < 3; i++) { setTimeout(() => console.log(i), 0); }` the output is:
- A) 0 1 2
- B) 1 2 3
- C) 3 3 3
- D) 0 0 0

### Answer Key
- Q1: **B**.
- Q2: **C**. The declaration is hoisted, the value is not.
- Q3: **A**.
- Q4: **C**. All callbacks see the same `i`, which ends at 3.
