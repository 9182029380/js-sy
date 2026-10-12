# Class 31: JavaScript Function - apply()

## 1. Definition
`apply()` is a function method that **invokes the function immediately** with a chosen `this` value and arguments passed **as an array** (or array-like object).

Syntax: `func.apply(thisArg, [arg1, arg2, ...])`

## 2. Usage
- Calling a function when the arguments are already in an array.
- Using `Math.max` / `Math.min` on arrays (older style).
- Method borrowing with a set of arguments.
- Forwarding all arguments in wrappers, decorators and middleware.

## 3. Description
- Works like `call()`, only the argument list is **one array**.
- Memory trick: **A**pply = **A**rray, **C**all = **C**omma-separated.
- The function runs **immediately**.
- Modern code usually prefers **spread**: `Math.max(...numbers)`. `apply()` is still useful in wrapper functions: `original.apply(this, arguments)`.
- Arrow functions ignore the `this` given to `apply()`.

## 4. Examples

### Example 1: Arguments as an array
```js
function order(item, qty) {
  return `${this.customer} ordered ${qty} x ${item}`;
}
const customer = { customer: "Meena" };
console.log(order.apply(customer, ["Laptop", 2]));
// Meena ordered 2 x Laptop
```

### Example 2: Math.max with an array
```js
const nums = [4, 19, 7, 12];
console.log(Math.max.apply(null, nums));   // 19
console.log(Math.min.apply(null, nums));   // 4
console.log(Math.max(...nums));            // 19 (modern equivalent)
```

### Example 3: Forwarding arguments in a wrapper (logging decorator)
```js
function withLogging(fn) {
  return function (...args) {
    console.log("Calling with", args);
    return fn.apply(this, args);
  };
}
const add = (a, b) => a + b;
const loggedAdd = withLogging(add);
console.log(loggedAdd(3, 4));
// Calling with [ 3, 4 ]
// 7
```

## 5. Assignments
1. Use `apply()` to find the maximum and minimum of an array of marks.
2. Write a function `fullAddress(city, state, pin)` that uses `this.street`. Call it using `apply()` for two different address objects.
3. Write a `timeIt(fn)` wrapper that logs how long `fn` takes and forwards arguments with `apply()`.
4. Create a table comparing `call`, `apply` and `bind` (when it runs, how arguments are passed, what it returns).

## 6. MCQs
**Q1.** `apply()` accepts arguments as:
- A) Comma-separated list
- B) An array
- C) An object only
- D) A string

**Q2.** What does `Math.max.apply(null, [1, 5, 3])` return?
- A) 1
- B) 3
- C) 5
- D) `NaN`

**Q3.** Does `apply()` call the function immediately?
- A) No, it returns a new function
- B) Yes
- C) Only if `this` is `null`
- D) Only in strict mode

**Q4.** The modern alternative to `Math.max.apply(null, arr)` is:
- A) `Math.max(arr)`
- B) `Math.max(...arr)`
- C) `Math.max[arr]`
- D) `max(arr)`

### Answer Key
- Q1: **B**.
- Q2: **C**.
- Q3: **B**.
- Q4: **B**. `Math.max(arr)` would give `NaN` for an array of several values.
