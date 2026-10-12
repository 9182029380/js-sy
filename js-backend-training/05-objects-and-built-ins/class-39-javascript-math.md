# Class 39: JavaScript Math

## 1. Definition
**Math** is a built-in object that provides mathematical constants and functions. It is not a constructor: you use it directly (`Math.round(4.6)`), never with `new`.

## 2. Usage
- Rounding prices and percentages.
- Random values (OTP, IDs, sampling, load balancing).
- Finding minimum and maximum of values.
- Calculations such as powers, roots, distances and averages.

## 3. Description

Constants: `Math.PI`, `Math.E`, `Math.SQRT2`.

| Method | Purpose | Example |
|---|---|---|
| `round(x)` | Nearest integer | `Math.round(4.5)` gives 5 |
| `floor(x)` | Round down | `Math.floor(-1.2)` gives -2 |
| `ceil(x)` | Round up | `Math.ceil(1.2)` gives 2 |
| `trunc(x)` | Remove decimals | `Math.trunc(-1.9)` gives -1 |
| `abs(x)` | Absolute value | `Math.abs(-5)` gives 5 |
| `max(...n)` / `min(...n)` | Largest / smallest | `Math.max(1, 9, 3)` gives 9 |
| `pow(a, b)` or `a ** b` | Power | `2 ** 3` gives 8 |
| `sqrt(x)`, `cbrt(x)` | Roots | `Math.sqrt(16)` gives 4 |
| `random()` | Random in `[0, 1)` | `0.3721...` |
| `sign(x)` | -1, 0 or 1 | `Math.sign(-8)` gives -1 |
| `sin`, `cos`, `log`, `log10`, `hypot` | Trig / logs | |

Tips:
- `Math.max()` with an array: `Math.max(...arr)`. Empty gives `-Infinity`.
- Random integer between `min` and `max` (inclusive): `Math.floor(Math.random() * (max - min + 1)) + min`.
- `Math.random()` is **not secure**. For tokens, OTPs or passwords in Node.js use `crypto.randomInt()` or `crypto.randomBytes()`.
- Round to 2 decimals: `Math.round(x * 100) / 100` or `x.toFixed(2)` (returns a string).

## 4. Examples

### Example 1: Rounding
```js
console.log(Math.round(4.5), Math.round(4.4));   // 5 4
console.log(Math.floor(-1.2), Math.ceil(-1.2));  // -2 -1
console.log(Math.trunc(-1.9));                   // -1
console.log(Math.round(2.34567 * 100) / 100);    // 2.35
```

### Example 2: Min, max, power and root
```js
const marks = [72, 91, 65, 88];
console.log(Math.max(...marks), Math.min(...marks));   // 91 65
console.log(2 ** 10, Math.pow(3, 3));                  // 1024 27
console.log(Math.sqrt(144), Math.abs(-7.5));           // 12 7.5
console.log(Math.hypot(3, 4));                         // 5
```

### Example 3: Random numbers
```js
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
console.log(randomInt(1, 6));      // dice roll 1..6

const otp = String(randomInt(0, 999999)).padStart(6, "0");
console.log(otp.length);           // 6 (demo only: use crypto in real systems)

const crypto = require("node:crypto");
console.log(crypto.randomInt(100000, 1000000));   // secure 6-digit number
```

## 5. Assignments
1. Write a function that returns the area and circumference of a circle for a given radius, rounded to 2 decimals.
2. Write `randomInt(min, max)` and use it to pick a random item from an array of names.
3. Calculate the distance between two points `(x1, y1)` and `(x2, y2)` using `Math.sqrt` and `Math.pow` (or `Math.hypot`).
4. Roll two dice 1000 times and count how often the sum is 7. Print the percentage.

## 6. MCQs
**Q1.** `Math.floor(4.9)` returns:
- A) 5
- B) 4
- C) 4.9
- D) 4.5

**Q2.** `Math.random()` returns a number:
- A) From 1 to 10
- B) From 0 up to but not including 1
- C) From 0 to 100
- D) Only integers

**Q3.** `Math.max()` with no arguments returns:
- A) 0
- B) `NaN`
- C) `-Infinity`
- D) `undefined`

**Q4.** Which is the best choice for generating a secure OTP in Node.js?
- A) `Math.random()`
- B) `Date.now()`
- C) `crypto.randomInt()`
- D) `Math.floor(1000)`

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **C**.
- Q4: **C**.
