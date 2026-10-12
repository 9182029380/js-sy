# Class 22: JavaScript for...of Loop

## 1. Definition
The **for...of loop** (ES6) iterates over the **values** of any **iterable** object: arrays, strings, Maps, Sets, `arguments`, generators and more.

## 2. Usage
- Looping over arrays of records (users, orders, products).
- Iterating characters in a string.
- Looping over `Map` and `Set` collections.
- Using `await` inside the loop to process items one by one (`for await...of` for async iterables).

## 3. Description
Syntax:
```js
for (const value of iterable) {
  // body
}
```
- Gives **values**, not indexes.
- Works with `break`, `continue` and `return` (unlike `forEach`).
- To get the index too, use `.entries()`: `for (const [i, v] of arr.entries())`.
- Plain objects are **not iterable**. Use `Object.keys()`, `Object.values()` or `Object.entries()`.
- Inside `async` functions, `await` works properly in `for...of` (it does not in `forEach`).

## 4. Examples

### Example 1: Arrays and strings
```js
for (const city of ["Hyderabad", "Pune", "Chennai"]) {
  console.log(city);
}
for (const ch of "JS") console.log(ch);   // J then S
```

### Example 2: Index with entries, Map and Set
```js
const tools = ["node", "npm", "git"];
for (const [i, tool] of tools.entries()) console.log(i, tool);

const stock = new Map([["pen", 10], ["book", 5]]);
for (const [item, qty] of stock) console.log(item, qty);

for (const n of new Set([1, 2, 2, 3])) console.log(n);   // 1 2 3
```

### Example 3: Sequential async work with await
```js
const wait = (ms) => new Promise((r) => setTimeout(r, ms));

async function run() {
  for (const id of [1, 2, 3]) {
    await wait(100);
    console.log("Processed order", id);
  }
}
run();
```

## 5. Assignments
1. Given an array of numbers, compute the sum and the maximum using `for...of`.
2. Count the vowels in a string using `for...of`.
3. Loop over `Object.entries({a:1, b:2, c:3})` with `for...of` and print `key = value`.
4. Write an `async` function that processes an array of three user IDs one at a time with a simulated 200 ms delay each, using `for...of` and `await`. Explain why `forEach` would not wait.

## 6. MCQs
**Q1.** `for...of` iterates over:
- A) Property names
- B) Values of an iterable
- C) Only objects
- D) Only numbers

**Q2.** Can `for...of` loop directly over a plain object `{a:1}`?
- A) Yes
- B) No, plain objects are not iterable
- C) Only in strict mode
- D) Only with `var`

**Q3.** Which lets you use `break` inside?
- A) `forEach`
- B) `for...of`
- C) `map`
- D) None

**Q4.** What does `for (const x of "abc")` iterate over?
- A) Indexes 0, 1, 2
- B) Characters
- C) Nothing, error
- D) Words

### Answer Key
- Q1: **B**.
- Q2: **B**. Use `Object.entries()` etc.
- Q3: **B**.
- Q4: **B**.
