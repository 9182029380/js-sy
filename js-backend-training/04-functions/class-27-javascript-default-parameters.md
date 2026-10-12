# Class 27: JavaScript Default Parameters

## 1. Definition
**Default parameters** (ES6) let you give a parameter an initial value that is used when the argument is **missing or `undefined`**.

## 2. Usage
- Optional settings (port, page size, timeout, currency).
- Safer functions that work without every argument.
- Replacing old code like `a = a || 10`.
- Default values for destructured options objects.

## 3. Description
Syntax:
```js
function name(param1 = defaultValue1, param2 = defaultValue2) { }
```
- Default applies **only for `undefined`**, not for `null`, `0`, `""` or `false`.
- Defaults are evaluated **at call time**, so they can be expressions or function calls.
- A default can use **earlier parameters**.
- Parameters with defaults are usually placed **last**.
- Combine with destructuring: `function f({ a = 1, b = 2 } = {})`.
- Old pattern `x = x || 5` wrongly replaces `0` and `""`. Defaults avoid this.

## 4. Examples

### Example 1: Basic defaults
```js
function greet(name = "Guest", greeting = "Hello") {
  return `${greeting}, ${name}!`;
}
console.log(greet());                 // Hello, Guest!
console.log(greet("Ravi"));           // Hello, Ravi!
console.log(greet("Ravi", "Welcome")); // Welcome, Ravi!
```

### Example 2: Only undefined triggers the default
```js
function show(v = "default") { console.log(v); }
show(undefined);   // default
show(null);        // null
show(0);           // 0
show("");          // (empty line)
```

### Example 3: Expressions, earlier params and options object
```js
function price(amount, tax = amount * 0.18) {
  return amount + tax;
}
console.log(price(1000));        // 1180
console.log(price(1000, 50));    // 1050

function connect({ host = "localhost", port = 5432 } = {}) {
  return `${host}:${port}`;
}
console.log(connect());                       // localhost:5432
console.log(connect({ host: "db.local" }));   // db.local:5432
```

## 5. Assignments
1. Write `paginate(page = 1, size = 10)` that returns `{ skip, limit }`. Test with and without arguments.
2. Write `createServer({ port = 3000, env = "dev" } = {})` returning a description string. Call it with no argument at all.
3. Show the problem with `x = x || 10` when `x` is `0`, then fix it with a default parameter.
4. Write a function where one default depends on an earlier parameter (for example `rectangle(width, height = width)`).

## 6. MCQs
**Q1.** When is a default value used?
- A) When the argument is `null`
- B) When the argument is `undefined`
- C) When the argument is `0`
- D) Always

**Q2.** `function f(a = 5) { return a; } f(null)` returns:
- A) 5
- B) `undefined`
- C) `null`
- D) 0

**Q3.** Can a default value refer to an earlier parameter?
- A) No
- B) Yes
- C) Only for numbers
- D) Only in arrow functions

**Q4.** What does `f()` return for `function f({ a = 1 } = {}) { return a; }`?
- A) `undefined`
- B) 1
- C) TypeError
- D) `null`

### Answer Key
- Q1: **B**.
- Q2: **C**. `null` is a value, so the default is not used.
- Q3: **B**.
- Q4: **B**. The `= {}` makes the whole argument optional too.
