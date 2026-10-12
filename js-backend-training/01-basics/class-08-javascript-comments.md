# Class 08: JavaScript Comments

## 1. Definition
A **comment** is text in the source code that the JavaScript engine ignores. It is written for humans to explain, document or temporarily disable code.

## 2. Usage
- Explain **why** code does something (not what it obviously does).
- Document functions, parameters and return values (JSDoc).
- Temporarily disable code while debugging.
- Mark pending work with `TODO` or `FIXME`.
- Provide editor hints and type information.

## 3. Description
Types of comments:

| Type | Syntax | Use |
|---|---|---|
| Single-line | `// comment` | Short notes |
| Multi-line | `/* comment */` | Longer explanations, can span lines (cannot be nested) |
| JSDoc | `/** ... */` | Documentation read by editors and doc tools |
| Shebang | `#!/usr/bin/env node` | First line of a CLI script on Linux/macOS |

Good commenting practice:
- Keep comments up to date. A wrong comment is worse than none.
- Do not comment obvious code (`i++ // add one`).
- Prefer clear names over comments, then add comments for intent and business rules.

## 4. Examples

### Example 1: Single-line and multi-line
```js
// Calculate GST for the order
const gst = 0.18;

/*
  Discount rules:
  - Premium users: 10%
  - New users: 5%
*/
const discount = 0.1;
console.log(gst, discount);
```

### Example 2: JSDoc for a function
```js
/**
 * Calculates the final bill amount.
 * @param {number} amount - Base amount in INR
 * @param {number} taxRate - Tax as a decimal, e.g. 0.18
 * @returns {number} Total payable amount
 */
function totalBill(amount, taxRate) {
  return amount + amount * taxRate;
}
console.log(totalBill(1000, 0.18));   // 1180
```
Hover over `totalBill` in VS Code to see the documentation.

### Example 3: Commenting out code and TODO
```js
function processOrder(order) {
  // TODO: add stock validation
  console.log("Processing", order.id);
  // console.log("Debug:", order);   // disabled while testing
}
processOrder({ id: 101 });
```

## 5. Assignments
1. Add single-line comments to a small program (calculating an average of five numbers) explaining each step's purpose.
2. Write a function `isAdult(age)` and document it fully with JSDoc (description, param, returns, example).
3. Take a 10-line script with bugs, comment out lines one at a time to find which line causes the error. Describe your approach.
4. Explain why `/* outer /* inner */ still outer */` causes an error. Prove it by running it.

## 6. MCQs
**Q1.** Which is a valid single-line comment?
- A) `<!-- comment -->`
- B) `# comment`
- C) `// comment`
- D) `** comment **`

**Q2.** What does `/** ... */` usually indicate?
- A) A syntax error
- B) A JSDoc documentation comment
- C) A string literal
- D) A regular expression

**Q3.** Which is true?
- A) Comments run before the code
- B) Comments slow down every request in production
- C) Comments are ignored by the engine
- D) Comments can be nested with `/* */`

**Q4.** What is the best use of a comment?
- A) Repeat what the code obviously does
- B) Explain why something is done a certain way
- C) Store passwords
- D) Replace variable names

### Answer Key
- Q1: **C**.
- Q2: **B**.
- Q3: **C**. Engines skip comments. Block comments cannot be nested.
- Q4: **B**.
