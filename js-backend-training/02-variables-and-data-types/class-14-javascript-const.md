# Class 14: JavaScript const

## 1. Definition
`const` (ES6 / ES2015) declares a **block-scoped** variable that **cannot be re-assigned**. It must be initialised at declaration.

## 2. Usage
- Configuration values, constants (`PORT`, `API_URL`).
- Imported modules: `const express = require("express");`
- Functions, arrow functions, arrays and objects that are not re-assigned.
- Modern guideline: **use `const` by default**, switch to `let` only when re-assignment is needed.

## 3. Description
- Must be initialised: `const x;` is a `SyntaxError`.
- Cannot be re-assigned: `x = 5;` throws a `TypeError`.
- Block scoped and has a Temporal Dead Zone like `let`.
- **`const` does not make values immutable.** For objects and arrays, the **reference** is fixed but the contents can change.
- To prevent changes to an object, use `Object.freeze(obj)` (shallow freeze).

## 4. Examples

### Example 1: Re-assignment is not allowed
```js
const PORT = 3000;
try {
  PORT = 4000;
} catch (e) {
  console.log(e.name + ": " + e.message);   // TypeError: Assignment to constant variable.
}
console.log(PORT);   // 3000
```

### Example 2: Objects and arrays can still change inside
```js
const user = { name: "Anil" };
user.name = "Ravi";           // allowed
user.city = "Hyderabad";      // allowed
console.log(user);

const list = [1, 2];
list.push(3);                 // allowed
console.log(list);            // [1, 2, 3]

// user = {};                 // TypeError (re-assignment)
```

### Example 3: Object.freeze for true protection
```js
const settings = Object.freeze({ mode: "prod", retries: 3 });
settings.mode = "dev";        // ignored silently (error in strict mode)
console.log(settings.mode);   // prod
console.log(Object.isFrozen(settings));   // true
```

## 5. Assignments
1. Create constants for `PI`, `TAX_RATE` and `APP_NAME`. Calculate the area of a circle with radius 7 and print it.
2. Show with code that a `const` array can be modified with `push` but not re-assigned. Explain why.
3. Freeze a config object and try modifying it. Run once normally and once with `"use strict";` and compare.
4. Take a script that uses `let` for every variable and convert each to `const` where possible. List which ones had to remain `let` and why.

## 6. MCQs
**Q1.** What happens with `const x;`?
- A) `x` is `undefined`
- B) `SyntaxError`
- C) `x` is `null`
- D) Works fine

**Q2.** Given `const arr = [1,2]; arr.push(3);` the result is:
- A) `TypeError`
- B) `arr` becomes `[1,2,3]`
- C) `arr` stays `[1,2]`
- D) `SyntaxError`

**Q3.** Which makes an object shallowly immutable?
- A) `const`
- B) `Object.freeze()`
- C) `let`
- D) `Object.lock()`

**Q4.** Which is the recommended default keyword in modern JS?
- A) `var`
- B) `let`
- C) `const`
- D) None, use implicit globals

### Answer Key
- Q1: **B**. A `const` must be initialised.
- Q2: **B**. Only re-assignment of the variable is blocked.
- Q3: **B**.
- Q4: **C**.
