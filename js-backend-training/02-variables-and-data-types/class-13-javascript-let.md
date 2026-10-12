# Class 13: JavaScript let

## 1. Definition
`let` (introduced in ES6 / ES2015) declares a **block-scoped** variable whose value can be changed (re-assigned) but which cannot be redeclared in the same scope.

## 2. Usage
- Counters and loop variables.
- Values that change over time (running totals, status flags, retry counts).
- Default choice when a variable must be re-assigned. Use `const` if it never changes.

## 3. Description
- **Block scope**: exists only inside the nearest `{ }` (if, for, while, plain block).
- **No redeclaration** in the same scope (`SyntaxError`).
- **Re-assignment allowed**.
- **Hoisted but not initialised**: accessing it before the declaration throws a `ReferenceError`. The gap is the **Temporal Dead Zone (TDZ)**.
- Each loop iteration gets its **own copy** of a `let` loop variable.
- A top-level `let` does not become a property of the global object.

## 4. Examples

### Example 1: Block scope
```js
let level = "outer";
if (true) {
  let level = "inner";       // separate variable
  console.log(level);        // inner
}
console.log(level);          // outer
```

### Example 2: Temporal Dead Zone
```js
try {
  console.log(total);   // ReferenceError
  let total = 100;
} catch (e) {
  console.log(e.name + ": " + e.message);
}
```

### Example 3: Per-iteration binding in loops
```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
// prints 0, 1, 2

let retries = 0;
while (retries < 3) {
  retries += 1;
}
console.log(retries);   // 3
```

## 5. Assignments
1. Write a loop that sums numbers 1 to 100 using `let sum`. Print the result.
2. Demonstrate block scope: declare `let x` in an `if` block and show it is not accessible outside (catch the `ReferenceError`).
3. Trigger the Temporal Dead Zone intentionally, and explain in two lines why it exists.
4. Re-write the `var` closure loop from Class 12 using `let` and explain the difference.

## 6. MCQs
**Q1.** `let` variables are scoped to:
- A) The whole file
- B) The enclosing function only
- C) The enclosing block
- D) The global object

**Q2.** What happens when you access a `let` variable before its declaration?
- A) Returns `undefined`
- B) Returns `null`
- C) Throws a `ReferenceError`
- D) Returns 0

**Q3.** Can you write `let a = 1; let a = 2;` in the same scope?
- A) Yes
- B) No, it is a `SyntaxError`
- C) Only in strict mode
- D) Only at the top level

**Q4.** Can a `let` variable be reassigned?
- A) Yes
- B) No
- C) Only once
- D) Only inside functions

### Answer Key
- Q1: **C**.
- Q2: **C**. This is the Temporal Dead Zone.
- Q3: **B**.
- Q4: **A**.
