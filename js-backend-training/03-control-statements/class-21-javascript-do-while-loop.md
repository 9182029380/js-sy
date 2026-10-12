# Class 21: JavaScript do-while Loop

## 1. Definition
The **do-while loop** runs the body first and then checks the condition. It guarantees the body executes **at least once**.

## 2. Usage
- Menus and prompts that must display at least once.
- Input validation (ask, then repeat if invalid).
- Polling or retry logic where the first attempt always happens.

## 3. Description
Syntax:
```js
do {
  // body runs at least once
} while (condition);
```
- Note the **semicolon** after `while (condition)`.
- If the condition is false from the start, the body still runs once.
- `break` and `continue` work as in other loops.
- Compare: `while` checks first (zero or more runs), `do...while` checks last (one or more runs).

## 4. Examples

### Example 1: Runs once even when the condition is false
```js
let i = 10;
do {
  console.log("i is", i);   // prints once
  i++;
} while (i < 5);
```

### Example 2: Counting
```js
let count = 1;
do {
  console.log("Count:", count);
  count++;
} while (count <= 3);
```

### Example 3: Validate until correct (simulated input)
```js
const inputs = ["abc", "", "42"];   // pretend user typed these
let idx = 0;
let value;
do {
  value = inputs[idx++];
  console.log("User entered:", JSON.stringify(value));
} while (isNaN(Number(value)) || value === "");
console.log("Accepted:", Number(value));
```

## 5. Assignments
1. Print numbers from 1 to 10 using `do...while`.
2. Write a number guessing simulation: the secret is 7, guesses come from an array. Loop until the guess matches and show attempts.
3. Show the difference between `while` and `do...while` using a condition that starts false. Explain the output.
4. Sum numbers from an array until the running total exceeds 100 using `do...while`.

## 6. MCQs
**Q1.** A `do...while` body runs at least:
- A) Zero times
- B) Once
- C) Twice
- D) Depends on the condition

**Q2.** Where is the condition checked?
- A) Before the body
- B) After the body
- C) Never
- D) Inside the body only

**Q3.** What does this print? `let x = 5; do { console.log(x); } while (x < 3);`
- A) Nothing
- B) 5
- C) 3
- D) Infinite output

**Q4.** Which loop checks the condition first?
- A) `do...while`
- B) `while`
- C) Both
- D) Neither

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **B**.
- Q4: **B**.
