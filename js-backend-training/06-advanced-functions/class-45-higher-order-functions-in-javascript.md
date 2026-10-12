# Class 45: Higher-Order Functions in JavaScript

## 1. Definition
A **higher-order function (HOF)** is a function that **takes one or more functions as arguments**, **returns a function**, or both.

## 2. Usage
- Data transformation pipelines: `map`, `filter`, `reduce`.
- Reusable behaviour wrappers: logging, timing, retry, caching, authentication checks.
- Middleware factories in Node.js (`rateLimit(100)` returns a middleware).
- Configurable utilities (`sortBy("price")`, `validator(rules)`).

## 3. Description
- Built-in HOFs: `map`, `filter`, `reduce`, `forEach`, `find`, `some`, `every`, `sort`, `flatMap`, plus `setTimeout`, `bind`.
- **Custom HOFs** let you separate *what to do* (the callback) from *how to loop or wrap* (the HOF).
- **Function composition**: combine small functions into bigger ones (`compose`, `pipe`).
- **Currying**: turn `f(a, b)` into `f(a)(b)`.
- Benefits: less repetition, declarative code, easier testing.
- Related: closures (returned functions remember the arguments), callbacks (the function arguments).

## 4. Examples

### Example 1: Built-in HOFs on data
```js
const employees = [
  { name: "Anil", dept: "Cloud", salary: 90000 },
  { name: "Ravi", dept: "Dev", salary: 70000 },
  { name: "Meena", dept: "Cloud", salary: 110000 }
];
const cloudTotal = employees
  .filter((e) => e.dept === "Cloud")
  .map((e) => e.salary)
  .reduce((sum, s) => sum + s, 0);
console.log(cloudTotal);   // 200000
```

### Example 2: A function that returns a function
```js
function greaterThan(limit) {
  return (n) => n > limit;
}
const above100 = greaterThan(100);
console.log([50, 150, 300].filter(above100));   // [150, 300]

const curriedAdd = (a) => (b) => a + b;
console.log(curriedAdd(5)(10));   // 15
```

### Example 3: Wrapper (decorator) and compose
```js
function withTiming(fn) {
  return function (...args) {
    const start = Date.now();
    const result = fn.apply(this, args);
    console.log(`${fn.name || "fn"} took ${Date.now() - start} ms`);
    return result;
  };
}
function slowSum(n) { let s = 0; for (let i = 1; i <= n; i++) s += i; return s; }
const timedSum = withTiming(slowSum);
console.log(timedSum(1_000_000));

const compose = (...fns) => (x) => fns.reduceRight((acc, f) => f(acc), x);
const trim = (s) => s.trim();
const upper = (s) => s.toUpperCase();
console.log(compose(upper, trim)("  hello  "));   // HELLO
```

## 5. Assignments
1. Write your own `myMap(array, fn)` and `myFilter(array, fn)` (no built-in `map`/`filter`).
2. Create `sortBy(key)` that returns a comparison function and use it to sort an array of products by `price` and by `name`.
3. Write a `retry(fn, times)` HOF that calls `fn` again if it throws, up to `times` attempts.
4. Use `reduce` to group an array of orders by `status` into an object of arrays. Compare with `Object.groupBy`.

## 6. MCQs
**Q1.** Which makes a function "higher-order"?
- A) It is long
- B) It takes or returns a function
- C) It uses `var`
- D) It has no parameters

**Q2.** Which is NOT a higher-order function?
- A) `arr.map(fn)`
- B) `arr.filter(fn)`
- C) `arr.push(5)`
- D) `arr.reduce(fn, 0)`

**Q3.** What does `const add = a => b => a + b; add(2)(3)` return?
- A) `2`
- B) `3`
- C) `5`
- D) A function

**Q4.** `compose` is used to:
- A) Declare classes
- B) Combine several functions into one
- C) Create arrays
- D) Delay execution

### Answer Key
- Q1: **B**.
- Q2: **C**. `push` takes a value, not a function.
- Q3: **C**.
- Q4: **B**.
