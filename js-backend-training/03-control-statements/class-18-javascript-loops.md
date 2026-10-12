# Class 18: JavaScript Loops

## 1. Definition
A **loop** repeats a block of code as long as a condition holds, or once for each item in a collection. It removes the need to write the same code many times.

## 2. Usage
- Processing lists of records from a database or API.
- Retrying failed operations.
- Generating reports, batches and paginated requests.
- Reading lines from files or streams.

## 3. Description
JavaScript loop types:

| Loop | Best for |
|---|---|
| `for` | Known number of iterations |
| `while` | Unknown number, check before running |
| `do...while` | Run at least once, check after |
| `for...of` | Values of arrays, strings, Maps, Sets |
| `for...in` | Keys (property names) of an object |
| `Array.forEach/map/filter/reduce` | Functional style on arrays |

Loop control:
- `break` exits the loop immediately.
- `continue` skips to the next iteration.
- Labels let you break from nested loops (`outer: for (...) { ... break outer; }`).
- **Infinite loop**: the condition never becomes false (e.g. forgetting to update the counter). Always make sure the condition can end.

## 4. Examples

### Example 1: Same task with three loops
```js
// Print 1 to 3
for (let i = 1; i <= 3; i++) console.log(i);

let j = 1;
while (j <= 3) { console.log(j); j++; }

let k = 1;
do { console.log(k); k++; } while (k <= 3);
```

### Example 2: break and continue
```js
for (let i = 1; i <= 10; i++) {
  if (i % 2 === 0) continue;   // skip even numbers
  if (i > 7) break;            // stop after 7
  console.log(i);              // 1 3 5 7
}
```

### Example 3: Choosing the right loop for the data
```js
const orders = [{ id: 1, amount: 500 }, { id: 2, amount: 800 }];
let total = 0;
for (const order of orders) total += order.amount;
console.log(total);   // 1300

const user = { name: "Ravi", city: "Hyderabad" };
for (const key in user) console.log(key, user[key]);
```

## 5. Assignments
1. Print the multiplication table of any number up to 10 using a loop.
2. Find the sum of all numbers from 1 to 1000 that are divisible by 3 or 5.
3. Use a nested loop to print a right-angled triangle of `*` with 5 rows.
4. Write a loop that searches an array for a value and stops as soon as it is found (use `break`). Print the index or `-1`.

## 6. MCQs
**Q1.** Which loop always runs its body at least once?
- A) `for`
- B) `while`
- C) `do...while`
- D) `for...of`

**Q2.** What does `continue` do?
- A) Exits the loop
- B) Skips the rest of the current iteration
- C) Restarts the program
- D) Ends the function

**Q3.** Which causes an infinite loop?
- A) `for (let i = 0; i < 3; i++) {}`
- B) `while (true) {}` without a `break`
- C) `for (const x of [])`
- D) `do {} while (false)`

**Q4.** Which loop is designed for array values?
- A) `for...in`
- B) `for...of`
- C) `while`
- D) `switch`

### Answer Key
- Q1: **C**.
- Q2: **B**.
- Q3: **B**.
- Q4: **B**.
