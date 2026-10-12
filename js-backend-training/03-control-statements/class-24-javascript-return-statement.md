# Class 24: JavaScript return Statement

## 1. Definition
The **return** statement ends the execution of a function and sends a value back to the caller. If no value is given, the function returns `undefined`.

## 2. Usage
- Returning computed results (totals, formatted text, database rows).
- Early exit (guard clauses) from a function when input is invalid.
- Returning objects, arrays, other functions or Promises.
- In `async` functions, the returned value is wrapped in a Promise.

## 3. Description
Syntax:
```js
function name(params) {
  return expression;
}
```
- Code after `return` in the same function is **never executed**.
- A function without `return` gives `undefined`.
- `return` can only return **one value**. To return multiple values, return an array or object.
- Arrow functions with one expression return it implicitly: `(a, b) => a + b`.
- To return an object literal from an arrow function wrap it in parentheses: `() => ({ ok: true })`.
- ASI trap: `return` followed by a newline returns `undefined`. Start the value on the same line.
- `return` inside a loop exits both the loop and the function.

## 4. Examples

### Example 1: Basic return
```js
function add(a, b) {
  return a + b;
}
const result = add(5, 7);
console.log(result);   // 12

function noReturn() { /* nothing */ }
console.log(noReturn());   // undefined
```

### Example 2: Early return and returning multiple values
```js
function divide(a, b) {
  if (b === 0) return { error: "Cannot divide by zero" };
  return { result: a / b };
}
console.log(divide(10, 2));   // { result: 5 }
console.log(divide(1, 0));    // { error: ... }

function minMax(arr) {
  return [Math.min(...arr), Math.max(...arr)];
}
const [min, max] = minMax([4, 9, 2]);
console.log(min, max);   // 2 9
```

### Example 3: Return in loops, arrow functions and async
```js
function findFirstEven(nums) {
  for (const n of nums) {
    if (n % 2 === 0) return n;   // exits loop and function
  }
  return null;
}
console.log(findFirstEven([1, 3, 6, 8]));   // 6

const makeUser = (name) => ({ name, active: true });
console.log(makeUser("Anil"));

async function getId() { return 101; }
getId().then((id) => console.log(id));   // 101
```

## 5. Assignments
1. Write `isPrime(n)` that returns `true` or `false`, using early `return`.
2. Write `stats(numbers)` returning an object with `sum`, `average`, `min` and `max`.
3. Create a function that returns another function (e.g. `multiplier(factor)` returning `n => n * factor`). Use it to create `double` and `triple`.
4. Demonstrate the ASI trap with a `return` on its own line, then fix it. Explain what the engine does.

## 6. MCQs
**Q1.** What does a function return when it has no `return` statement?
- A) `null`
- B) `0`
- C) `undefined`
- D) An empty object

**Q2.** What happens to code after `return` in the same function?
- A) It runs after the caller finishes
- B) It never runs
- C) It runs twice
- D) It throws an error

**Q3.** Which correctly returns an object from an arrow function?
- A) `() => { ok: true }`
- B) `() => ({ ok: true })`
- C) `() => return { ok: true }`
- D) `=> ok: true`

**Q4.** An `async` function that does `return 5` gives the caller:
- A) The number 5
- B) A Promise that resolves to 5
- C) `undefined`
- D) An error

### Answer Key
- Q1: **C**.
- Q2: **B**.
- Q3: **B**. Without parentheses the braces are read as a function body.
- Q4: **B**.
