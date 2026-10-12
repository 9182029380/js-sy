# Class 25: JavaScript Functions

## 1. Definition
A **function** is a reusable block of code that performs a task. It runs when it is **called (invoked)**, can accept inputs (**parameters**) and can give back an output (**return value**).

## 2. Usage
- Avoiding repeated code (write once, use many times).
- Organising logic: validation, calculation, formatting, database access.
- Route handlers, middleware, event handlers and callbacks in Node.js.
- Building blocks for modules and services.

## 3. Description
Ways to create functions:

| Style | Syntax | Hoisted? |
|---|---|---|
| Function declaration | `function add(a, b) { return a + b; }` | Yes (fully) |
| Function expression | `const add = function (a, b) { return a + b; };` | No |
| Arrow function | `const add = (a, b) => a + b;` | No |
| Method in object/class | `{ add(a, b) { ... } }` | n/a |

Key points:
- **Parameters** are the names in the definition. **Arguments** are the actual values passed when calling.
- A function is an **object** and a value: it can be stored in variables, passed, returned.
- **Local scope**: variables declared inside are not visible outside.
- Name functions with **verbs** (`calculateTotal`, `getUser`).
- Keep functions small and focused on one job.

## 4. Examples

### Example 1: Declaration and call
```js
function greet(name) {
  return `Hello, ${name}!`;
}
console.log(greet("Ravi"));   // Hello, Ravi!
console.log(greet("Anil"));   // Hello, Anil!
```

### Example 2: Expression vs arrow
```js
const square = function (n) { return n * n; };
const cube = (n) => n * n * n;
console.log(square(4), cube(3));   // 16 27
```

### Example 3: Local scope and reuse
```js
function totalWithTax(amount, rate = 0.18) {
  const tax = amount * rate;     // local variable
  return amount + tax;
}
console.log(totalWithTax(1000));        // 1180
console.log(totalWithTax(1000, 0.05));  // 1050
// console.log(tax);   // ReferenceError (tax is local)
```

## 5. Assignments
1. Write a function `isEven(n)` and use it to print the evens from 1 to 20.
2. Write a function `fullName(first, last)` that returns a formatted name in `LAST, First` style.
3. Create a function `calculateBill(price, qty, discountPercent)` that returns the final amount after discount. Call it with three different inputs.
4. Write the same `average(a, b, c)` function as a declaration, an expression and an arrow function. Test all three.

## 6. MCQs
**Q1.** What is the term for values passed when calling a function?
- A) Parameters
- B) Arguments
- C) Properties
- D) Returns

**Q2.** Which keyword sends a value back from a function?
- A) `send`
- B) `output`
- C) `return`
- D) `yield only`

**Q3.** Which function style is fully hoisted?
- A) Arrow function
- B) Function expression
- C) Function declaration
- D) None

**Q4.** Variables declared inside a function are:
- A) Global
- B) Local to that function
- C) Shared by all functions
- D) Constants

### Answer Key
- Q1: **B**. Parameters are the names in the definition.
- Q2: **C**.
- Q3: **C**.
- Q4: **B**.
