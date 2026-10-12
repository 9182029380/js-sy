# Class 44: Callback Function in JavaScript

## 1. Definition
A **callback function** is a function passed as an argument to another function, to be **called back later**, either immediately (synchronous) or when an operation finishes (asynchronous).

## 2. Usage
- Asynchronous work: file reads, database queries, HTTP calls, timers.
- Array methods: `map`, `filter`, `forEach`, `sort`.
- Event listeners and Express route handlers/middleware.
- Customising behaviour: validation, sorting rules, retry hooks.

## 3. Description
- Possible because **functions are first-class values**.
- **Synchronous callbacks** run during the call (`arr.map(cb)`).
- **Asynchronous callbacks** run later (`setTimeout(cb, 1000)`, `fs.readFile(path, cb)`).
- **Node.js error-first convention**: `callback(err, result)`. Check `err` first.
- **Callback hell** (pyramid of doom): deeply nested callbacks that are hard to read and maintain. Solutions: named functions, **Promises**, **async/await**.
- Pass a function **reference** (`cb`), do not call it (`cb()`), when giving it as an argument.
- Always call a callback **once**, and keep it consistently sync or async.

## 4. Examples

### Example 1: Synchronous callback
```js
function processNumbers(numbers, callback) {
  const out = [];
  for (const n of numbers) out.push(callback(n));
  return out;
}
console.log(processNumbers([1, 2, 3], (n) => n * 10));   // [10, 20, 30]
console.log([3, 1, 2].sort((a, b) => b - a));            // [3, 2, 1]
```

### Example 2: Asynchronous, error-first callback
```js
function getUser(id, callback) {
  setTimeout(() => {
    if (id <= 0) return callback(new Error("Invalid id"));
    callback(null, { id, name: "User" + id });
  }, 100);
}
getUser(5, (err, user) => {
  if (err) return console.error("Error:", err.message);
  console.log("Got", user);
});
getUser(-1, (err) => console.error("Error:", err.message));
```

### Example 3: Callback hell vs Promise/async
```js
const step = (label, cb) => setTimeout(() => cb(label), 50);

// Nested callbacks
step("A", (a) => {
  step("B", (b) => {
    step("C", (c) => console.log("Callbacks:", a, b, c));
  });
});

// Same flow with async/await
const stepP = (label) => new Promise((res) => setTimeout(() => res(label), 50));
(async () => {
  const a = await stepP("A");
  const b = await stepP("B");
  const c = await stepP("C");
  console.log("Async/await:", a, b, c);
})();
```

## 5. Assignments
1. Write `repeat(n, callback)` that calls the callback `n` times, passing the iteration number.
2. Write `filterBy(array, predicateCallback)` as your own version of `filter`.
3. Simulate `fetchOrder(id, callback)` and `fetchCustomer(order, callback)` with `setTimeout`. Chain them in nested style, then rewrite with Promises.
4. Using Node's `fs`, read a text file with `fs.readFile(path, "utf8", callback)` and handle both an existing and a non-existing file with the error-first pattern.

## 6. MCQs
**Q1.** A callback is:
- A) A function passed to another function to be called later
- B) A function that returns a Promise
- C) A loop
- D) A variable type

**Q2.** In Node.js error-first style, the first callback argument is:
- A) The result
- B) The error (or `null`)
- C) The next callback
- D) The status code

**Q3.** "Callback hell" refers to:
- A) A syntax error
- B) Deeply nested callbacks that are hard to read
- C) Missing callbacks
- D) Callbacks that run twice

**Q4.** Which is correct for passing a callback?
- A) `setTimeout(sayHi(), 1000)`
- B) `setTimeout(sayHi, 1000)`
- C) `setTimeout(sayHi[], 1000)`
- D) `setTimeout(call sayHi, 1000)`

### Answer Key
- Q1: **A**.
- Q2: **B**.
- Q3: **B**.
- Q4: **B**. Option A calls `sayHi` immediately and passes its result.
