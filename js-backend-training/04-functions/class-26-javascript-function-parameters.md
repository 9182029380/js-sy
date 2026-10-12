# Class 26: JavaScript Function Parameters

## 1. Definition
**Parameters** are the named inputs listed in a function definition. **Arguments** are the actual values supplied when the function is called. JavaScript is flexible: you can pass fewer or more arguments than declared.

## 2. Usage
- Making functions reusable with different inputs.
- Accepting options objects in APIs and services.
- Variable-length inputs (logging, sum of many numbers).
- Destructuring request bodies, config and query parameters.

## 3. Description
- **Missing arguments** become `undefined`.
- **Extra arguments** are ignored (but available via `arguments` or rest parameters).
- **Pass by value for primitives, pass by reference for objects**. Changing a property of an object parameter affects the original.
- **Rest parameters** `...args` collect extra arguments into a real array.
- **Spread** `...array` expands an array into separate arguments when calling.
- **Destructured parameters** let you unpack an object or array directly in the signature.
- The `arguments` object exists in regular functions (not arrow functions). Prefer rest parameters.
- For more than 3 parameters, pass a single **options object**.

## 4. Examples

### Example 1: Missing and extra arguments
```js
function show(a, b) {
  console.log(a, b);
}
show(1);          // 1 undefined
show(1, 2, 3);    // 1 2 (3 is ignored)
```

### Example 2: Rest and spread
```js
function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}
console.log(sum(1, 2, 3, 4));   // 10

const values = [5, 10, 15];
console.log(sum(...values));    // 30
```

### Example 3: Destructured options object and reference behaviour
```js
function createUser({ name, role = "user", active = true }) {
  return { name, role, active };
}
console.log(createUser({ name: "Anil" }));
console.log(createUser({ name: "Ravi", role: "admin" }));

function rename(user) { user.name = "Changed"; }
const u = { name: "Original" };
rename(u);
console.log(u.name);   // Changed (objects are passed by reference)
```

## 5. Assignments
1. Write `maxOf(...nums)` that returns the largest number using rest parameters.
2. Write `describePerson({ name, age, city })` that returns a sentence from a destructured object.
3. Demonstrate that primitives are passed by value and objects by reference with two small functions.
4. Create a `logMessage(level, ...parts)` function that prints `[LEVEL] part1 part2 ...` for any number of parts.

## 6. MCQs
**Q1.** If a function expects 2 parameters and you pass 1 argument, the second parameter is:
- A) `null`
- B) `0`
- C) `undefined`
- D) Error is thrown

**Q2.** What does `...args` in a function definition do?
- A) Spreads an array
- B) Collects the remaining arguments into an array
- C) Declares a constant
- D) Copies an object

**Q3.** Objects passed to a function are:
- A) Always copied
- B) Passed by reference
- C) Frozen
- D) Converted to strings

**Q4.** Which function type does NOT have its own `arguments` object?
- A) Function declaration
- B) Function expression
- C) Arrow function
- D) Method

### Answer Key
- Q1: **C**.
- Q2: **B**. This is a rest parameter.
- Q3: **B**. The reference is copied, so both names point to the same object.
- Q4: **C**.
