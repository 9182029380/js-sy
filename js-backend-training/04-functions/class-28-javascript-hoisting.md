# Class 28: JavaScript Hoisting

## 1. Definition
**Hoisting** is JavaScript's behaviour of processing declarations before running any code, so declarations appear to be "moved to the top" of their scope.

## 2. Usage
- Understanding why some code works before it is defined and other code throws errors.
- Debugging `undefined` and `ReferenceError` problems.
- Deciding how to order functions and variables in a file.
- Common interview topic.

## 3. Description
What happens for each declaration type:

| Declaration | Hoisted? | Before declaration line |
|---|---|---|
| `function name() {}` | Yes, with its body | Can be called |
| `var x` | Yes, initialised to `undefined` | Value is `undefined` |
| `let x` / `const x` | Hoisted but **not initialised** (TDZ) | `ReferenceError` |
| `class A {}` | Hoisted but in TDZ | `ReferenceError` |
| Function expression `var f = function(){}` | Only the `var` name is hoisted | `TypeError: f is not a function` |
| Arrow function `const f = () => {}` | Behaves like `const` | `ReferenceError` |

- Only **declarations** are hoisted, **not assignments**.
- Function declarations win over `var` with the same name when hoisting, then assignments run in order.
- Best practice: declare variables at the top of their scope, define functions before use, use `const` and `let`.

## 4. Examples

### Example 1: Function declaration vs expression
```js
console.log(add(2, 3));   // 5 (declaration is fully hoisted)
function add(a, b) { return a + b; }

try {
  multiply(2, 3);
} catch (e) {
  console.log(e.name);    // TypeError (var multiply is undefined)
}
var multiply = function (a, b) { return a * b; };
```

### Example 2: var vs let/const
```js
console.log(a);   // undefined
var a = 10;

try {
  console.log(b);
} catch (e) {
  console.log(e.name);   // ReferenceError
}
let b = 20;
```

### Example 3: Hoisting inside a function
```js
function test() {
  console.log(msg);   // undefined
  var msg = "hi";
  console.log(msg);   // hi
}
test();

// What the engine effectively sees:
// function test() { var msg; console.log(msg); msg = "hi"; console.log(msg); }
```

## 5. Assignments
1. Predict the output of five small snippets mixing `var`, `let`, function declarations and expressions. Run each and compare.
2. Show a function declaration being called before it is written and explain why it works.
3. Rewrite a snippet that relies on hoisting so that it declares everything before use.
4. Write a short explanation (5 lines) of the Temporal Dead Zone with a code example that throws a `ReferenceError`.

## 6. MCQs
**Q1.** What does `console.log(x); var x = 5;` print?
- A) 5
- B) `ReferenceError`
- C) `undefined`
- D) `null`

**Q2.** Which can be called before its definition appears in the file?
- A) Arrow function in a `const`
- B) Function declaration
- C) Function expression in a `let`
- D) Class declaration

**Q3.** Accessing a `let` variable before declaration gives:
- A) `undefined`
- B) `ReferenceError`
- C) `0`
- D) `NaN`

**Q4.** Calling `f()` before `var f = function () {}` throws:
- A) `ReferenceError`
- B) `TypeError`
- C) `SyntaxError`
- D) Nothing

### Answer Key
- Q1: **C**.
- Q2: **B**.
- Q3: **B**.
- Q4: **B**. `f` exists (as `undefined`) but is not yet a function.
