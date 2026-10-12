# Class 19: JavaScript for Loop

## 1. Definition
The **for loop** repeats code a known number of times. It combines initialisation, condition and update in one line.

## 2. Usage
- Iterating over arrays by index.
- Counting, batching (process 100 records at a time) and pagination.
- Generating sequences, tables and patterns.
- Nested loops for matrices and grids.

## 3. Description
Syntax:
```js
for (initialisation; condition; update) {
  // body
}
```
Execution order:
1. Initialisation runs **once**.
2. Condition is checked. If false, the loop ends.
3. Body runs.
4. Update runs, go back to step 2.

Notes:
- Use `let` for the counter so it is block scoped.
- Any of the three parts can be omitted: `for (;;)` is an infinite loop.
- Count down with `i--`, or step with `i += 2`.
- Cache `arr.length` only for very hot loops, otherwise write it normally.

## 4. Examples

### Example 1: Basic counting
```js
for (let i = 1; i <= 5; i++) {
  console.log("Count:", i);
}
```

### Example 2: Looping over an array by index
```js
const servers = ["alpha", "beta", "gamma"];
for (let i = 0; i < servers.length; i++) {
  console.log(`${i}: ${servers[i]}`);
}
```

### Example 3: Counting down, steps and nested loops
```js
for (let i = 10; i >= 0; i -= 5) console.log(i);   // 10 5 0

for (let row = 1; row <= 3; row++) {
  let line = "";
  for (let col = 1; col <= row; col++) line += "* ";
  console.log(line);
}
// *
// * *
// * * *
```

## 5. Assignments
1. Print all even numbers between 1 and 50 using a `for` loop.
2. Calculate the factorial of a number (for example 6) using `for`.
3. Reverse a string without using the built-in `reverse()` method (loop from the last index).
4. Print the first 10 numbers of the Fibonacci series.

## 6. MCQs
**Q1.** In `for (let i = 0; i < 3; i++)`, how many times does the body run?
- A) 2
- B) 3
- C) 4
- D) Infinite

**Q2.** Which part of the `for` loop runs only once?
- A) Condition
- B) Update
- C) Initialisation
- D) Body

**Q3.** What does `for (;;) {}` do?
- A) Syntax error
- B) Runs forever unless `break` is used
- C) Never runs
- D) Runs once

**Q4.** Which prints `10 8 6 4 2`?
- A) `for (let i=10; i>0; i-=2)`
- B) `for (let i=10; i>0; i--)`
- C) `for (let i=2; i<=10; i+=2)`
- D) `for (let i=0; i<10; i+=2)`

### Answer Key
- Q1: **B**.
- Q2: **C**.
- Q3: **B**.
- Q4: **A**.
