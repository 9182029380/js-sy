# Class 06: JavaScript Syntax

## 1. Definition
**Syntax** is the set of rules that define how JavaScript programs are written: how statements, expressions, identifiers, literals and blocks must be structured so the engine can understand them.

## 2. Usage
Every JS file you write in Node.js or the browser depends on these rules. Syntax mistakes cause `SyntaxError` and the program does not run.

## 3. Description
Key rules:
- **Statements** perform actions and usually end with `;` (semicolons are optional but recommended, see ASI below).
- **Case sensitive**: `name`, `Name` and `NAME` are three different identifiers.
- **Identifiers** (names) start with a letter, `_` or `$`, then may contain digits. Reserved words (`class`, `function`, `return`) cannot be used.
- **Naming convention**: `camelCase` for variables and functions, `PascalCase` for classes, `UPPER_SNAKE_CASE` for constants.
- **Literals**: fixed values such as `10`, `"text"`, `true`, `[1,2]`, `{a:1}`.
- **Blocks** `{ ... }` group statements.
- **Whitespace** is mostly ignored, but keep code readable (2 spaces indentation is common).
- **Strict mode** (`"use strict";`) catches silent mistakes. ES modules and classes are strict automatically.
- **ASI (Automatic Semicolon Insertion)**: the engine inserts semicolons in some places, which can cause surprises. For example, a `return` followed by a new line returns `undefined`.

## 4. Examples

### Example 1: Statements, case sensitivity and naming
```js
const userName = "Anil";
const username = "Ravi";   // different identifier
console.log(userName, username);   // Anil Ravi

const MAX_RETRIES = 3;
class OrderService {}
```

### Example 2: Blocks and strict mode
```js
"use strict";
if (true) {
  const msg = "Inside a block";
  console.log(msg);
}
// undeclaredVar = 5;   // in strict mode: ReferenceError
```

### Example 3: The ASI trap
```js
function getA() {
  return
  { value: 1 };
}
function getB() {
  return {
    value: 1
  };
}
console.log(getA());   // undefined
console.log(getB());   // { value: 1 }
```
The opening `{` must be on the same line as `return`.

## 5. Assignments
1. List five valid and five invalid identifier names with a reason for each invalid one. Test them in Node.
2. Declare variables for a product (name, price, inStock) following proper naming conventions, then print one formatted sentence using them.
3. Create a file that contains a deliberate syntax error, read the error message Node gives, then fix it.
4. Demonstrate the ASI problem with `return`, then rewrite it correctly. Explain why it happens.

## 6. MCQs
**Q1.** Which is a valid JS identifier?
- A) `2total`
- B) `total-amount`
- C) `$total`
- D) `class`

**Q2.** JavaScript is:
- A) Case insensitive
- B) Case sensitive
- C) Case sensitive only in strict mode
- D) Case sensitive only for functions

**Q3.** What does `function f() { return \n 5; }` return when called?
- A) 5
- B) `undefined`
- C) `null`
- D) SyntaxError

**Q4.** What does `"use strict";` do?
- A) Makes code run faster
- B) Enables stricter error checking
- C) Disables semicolons
- D) Imports a module

### Answer Key
- Q1: **C**. Identifiers cannot start with a digit, contain `-`, or be reserved words.
- Q2: **B**.
- Q3: **B**. ASI inserts a semicolon after `return`.
- Q4: **B**.
