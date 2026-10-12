# Class 15: Difference between var, let and const in JavaScript

## 1. Definition
`var`, `let` and `const` are the three keywords for declaring variables. They differ in **scope**, **hoisting behaviour**, **re-declaration** and **re-assignment** rules.

## 2. Usage
- Choose the correct keyword for every variable you write.
- Debug scope and hoisting bugs.
- Frequently asked in interviews and code reviews.

## 3. Description

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Introduced | ES1 | ES6 (2015) | ES6 (2015) |
| Scope | Function / global | Block | Block |
| Hoisting | Hoisted, initialised as `undefined` | Hoisted, in TDZ (error if used early) | Hoisted, in TDZ |
| Re-declaration (same scope) | Allowed | Not allowed | Not allowed |
| Re-assignment | Allowed | Allowed | Not allowed |
| Initialisation required | No | No | **Yes** |
| Top-level becomes global property (browser) | Yes | No | No |
| Recommended | Avoid in new code | When value changes | **Default choice** |

**Rule of thumb**: start with `const`; use `let` if you must re-assign; avoid `var`.

## 4. Examples

### Example 1: Scope comparison
```js
function scopeTest() {
  if (true) {
    var a = "var";
    let b = "let";
    const c = "const";
  }
  console.log(a);                  // var
  try { console.log(b); } catch (e) { console.log("b:", e.name); }   // b: ReferenceError
  try { console.log(c); } catch (e) { console.log("c:", e.name); }   // c: ReferenceError
}
scopeTest();
```

### Example 2: Hoisting and re-declaration
```js
console.log(x);        // undefined
var x = 1;
var x = 2;             // OK

try {
  console.log(y);      // ReferenceError (TDZ)
  let y = 1;
} catch (e) {
  console.log(e.name);
}
// let y = 3; let y = 4;   // SyntaxError if uncommented in the same scope
```

### Example 3: Re-assignment
```js
let score = 10;
score = 20;            // fine

const limit = 100;
try { limit = 200; } catch (e) { console.log(e.name); }   // TypeError

var legacy = "a";
legacy = "b";          // fine
```

## 5. Assignments
1. Build a three-column table from memory (scope, hoisting, re-declaration) without looking at the notes, then check your answers.
2. Write one script that proves each of these: `var` leaks out of a block, `let` does not, `const` cannot be re-assigned.
3. Refactor this code to use the best keyword for each variable: `var total = 0; var items = [1,2,3]; for (var i = 0; i < items.length; i++) { total += items[i]; } var message = "Total: " + total;`
4. Explain, with code, why `let` in a `for` loop fixes the `setTimeout` closure issue that `var` has.

## 6. MCQs
**Q1.** Which is block scoped?
- A) `var` only
- B) `let` and `const`
- C) `var` and `let`
- D) All three

**Q2.** Which keyword allows re-declaration in the same scope?
- A) `let`
- B) `const`
- C) `var`
- D) None

**Q3.** Accessing a variable before its `let` declaration gives:
- A) `undefined`
- B) `null`
- C) `ReferenceError`
- D) `0`

**Q4.** Which statement is true?
- A) `const` objects cannot have properties changed
- B) `const` variables cannot be re-assigned
- C) `let` cannot be re-assigned
- D) `var` is block scoped

### Answer Key
- Q1: **B**.
- Q2: **C**.
- Q3: **C**.
- Q4: **B**. `const` blocks re-assignment, but object contents can still change.
