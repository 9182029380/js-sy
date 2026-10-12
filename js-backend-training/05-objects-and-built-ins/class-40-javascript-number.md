# Class 40: JavaScript Number

## 1. Definition
**Number** is the primitive type for integers and decimal values. All numbers use the 64-bit **IEEE 754 floating-point** format. The `Number` object provides constants and helper methods.

## 2. Usage
- Prices, quantities, ages, scores, percentages.
- Parsing and validating numeric input from forms and APIs.
- Formatting currency and decimals for display.
- Checking for invalid results (`NaN`, `Infinity`).

## 3. Description
- **Literals**: `42`, `3.14`, `1e6`, `0xFF` (hex), `0b101` (binary), `1_000_000` (separators).
- **Special values**: `NaN` (not a number), `Infinity`, `-Infinity`.
- `NaN !== NaN`. Check with `Number.isNaN(x)`.
- **Constants**: `Number.MAX_SAFE_INTEGER` (9007199254740991), `Number.EPSILON`, `Number.MIN_VALUE`.
- **Floating-point precision**: `0.1 + 0.2` is `0.30000000000000004`. For money, store the smallest unit (paise or cents) as integers.
- **Static methods**: `Number.isInteger()`, `Number.isFinite()`, `Number.isSafeInteger()`, `Number.parseFloat()`, `Number.parseInt()`.
- **Instance methods**: `toFixed(n)` (returns a **string**), `toPrecision(n)`, `toString(radix)`, `toLocaleString("en-IN")`.
- **Conversion**: `Number("42")` gives 42, `Number("")` gives 0, `Number("abc")` gives `NaN`, `parseInt("42px")` gives 42, unary `+"42"` gives 42.
- Use **BigInt** (`123n`) for integers beyond the safe range.

## 4. Examples

### Example 1: Special values and checks
```js
console.log(1 / 0, -1 / 0);                 // Infinity -Infinity
console.log(0 / 0, NaN === NaN);            // NaN false
console.log(Number.isNaN(NaN), Number.isNaN("abc"));   // true false
console.log(Number.isInteger(5), Number.isInteger(5.5)); // true false
console.log(Number.isFinite(100), Number.isFinite(Infinity));   // true false
```

### Example 2: Conversion and formatting
```js
console.log(Number("42"), Number("abc"), Number(""));   // 42 NaN 0
console.log(parseInt("42px"), parseFloat("3.14abc"));   // 42 3.14
console.log((1234.5678).toFixed(2));                    // "1234.57"
console.log((255).toString(16), (255).toString(2));     // ff 11111111
console.log((1234567.891).toLocaleString("en-IN"));     // 12,34,567.891
console.log(Number.MAX_SAFE_INTEGER);
```

### Example 3: Floating point and money
```js
console.log(0.1 + 0.2);                              // 0.30000000000000004
console.log(Math.abs(0.1 + 0.2 - 0.3) < Number.EPSILON);   // true

// Safer money handling: use whole paise
const priceInPaise = 1999;        // INR 19.99
const qty = 3;
const total = priceInPaise * qty; // 5997
console.log(`Total: INR ${(total / 100).toFixed(2)}`);   // Total: INR 59.97

console.log(9007199254740993n + 2n);   // BigInt for very large integers
```

## 5. Assignments
1. Write `safeNumber(input)` that returns a number or `null` for invalid input. Test with `"12"`, `" 7 "`, `""`, `"abc"`, `"4px"` and `null`.
2. Format 1234567.5 as Indian currency using `toLocaleString` with `style: "currency"` and `currency: "INR"`.
3. Show two examples of floating-point error and fix one using integers (paise) and the other using `toFixed`.
4. Convert a decimal number to binary, octal and hexadecimal, and convert a binary string back with `parseInt(str, 2)`.

## 6. MCQs
**Q1.** What does `Number.isNaN("abc")` return?
- A) `true`
- B) `false`
- C) `undefined`
- D) Error

**Q2.** `(3.14159).toFixed(2)` returns:
- A) `3.14` (number)
- B) `"3.14"` (string)
- C) `3.1`
- D) `"3.141"`

**Q3.** What is `NaN === NaN`?
- A) `true`
- B) `false`
- C) `undefined`
- D) Error

**Q4.** How should you store money to avoid float errors?
- A) As floating point decimals
- B) As strings only
- C) As integers of the smallest unit (e.g. paise)
- D) As `Infinity`

### Answer Key
- Q1: **B**. `Number.isNaN` does not convert, and `"abc"` is a string, not the value `NaN`. The global `isNaN("abc")` would return `true`.
- Q2: **B**.
- Q3: **B**.
- Q4: **C**.
