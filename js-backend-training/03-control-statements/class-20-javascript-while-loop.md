# Class 20: JavaScript while Loop

## 1. Definition
The **while loop** repeats a block of code **as long as its condition is true**. The condition is checked **before** each iteration, so the body may run zero times.

## 2. Usage
- Repeating until something happens (a queue is empty, a job succeeds, a flag changes).
- Retry logic with an attempt limit.
- Reading data until the end is reached.
- Algorithms where the number of iterations is not known in advance.

## 3. Description
Syntax:
```js
while (condition) {
  // body
}
```
- Make sure something inside the loop changes the condition, or you create an **infinite loop**.
- Use `break` for early exit, `continue` to skip an iteration.
- Prefer `for` when the count is known. Prefer `while` when it depends on a condition.

## 4. Examples

### Example 1: Basic while
```js
let n = 1;
while (n <= 5) {
  console.log(n);
  n++;
}
```

### Example 2: Processing a queue until empty
```js
const queue = ["job1", "job2", "job3"];
while (queue.length > 0) {
  const job = queue.shift();
  console.log("Processing", job);
}
console.log("Queue empty");
```

### Example 3: Retry with a limit
```js
let attempts = 0;
let success = false;
while (!success && attempts < 3) {
  attempts++;
  success = attempts === 3;   // pretend it works on the third try
  console.log(`Attempt ${attempts}: ${success ? "OK" : "failed"}`);
}
```

## 5. Assignments
1. Sum the digits of a number (for example 4825 gives 19) using a `while` loop with `%` and `Math.floor`.
2. Reverse a number (1234 gives 4321) using `while`.
3. Keep halving a number until it is less than 1 and count how many steps it takes.
4. Simulate a retry mechanism that tries up to 5 times and stops early when a random number is greater than 0.7. Print the attempts used.

## 6. MCQs
**Q1.** When is the `while` condition checked?
- A) After the body
- B) Before each iteration
- C) Only once
- D) Never

**Q2.** What happens with `while (false) { ... }`?
- A) Body runs once
- B) Body never runs
- C) Syntax error
- D) Infinite loop

**Q3.** Which causes an infinite loop?
- A) `let i=0; while (i<3) { i++; }`
- B) `let i=0; while (i<3) { }`
- C) `let i=3; while (i>0) { i--; }`
- D) `while (false) {}`

**Q4.** Which keyword leaves a `while` loop early?
- A) `exit`
- B) `stop`
- C) `break`
- D) `return` is the only way

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **B**. `i` never changes.
- Q4: **C**. (`return` also exits if inside a function, but `break` is the loop keyword.)
