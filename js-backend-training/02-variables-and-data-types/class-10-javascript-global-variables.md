# Class 10: JavaScript Global Variables

## 1. Definition
A **global variable** is declared outside any function or block and can be accessed from anywhere in the program. Its scope is the **global scope**.

## 2. Usage
- Application-wide constants (app name, default limits).
- Shared configuration loaded once at startup.
- Understanding global scope helps you avoid bugs like accidental globals and name collisions in large backend projects.

## 3. Description
- **Browser**: the global object is `window` (and `globalThis`). Top-level `var` becomes a property of `window`.
- **Node.js**: each file is a **module** with its own scope, so top-level variables are **not** truly global. The global object is `globalThis` (also `global`).
- Variables declared with `let` and `const` at the top level do not become properties of the global object.
- **Accidental global**: assigning to an undeclared name (`count = 5;`) creates a global in sloppy mode. Strict mode throws a `ReferenceError`.
- **Problems with globals**: name clashes, hard to test, hard to trace changes. Prefer modules and passing values.
- Use `globalThis` to access the global object in any environment.

## 4. Examples

### Example 1: Global vs local scope
```js
const appName = "OrderService";   // global to this file

function printName() {
  console.log(appName);           // accessible here
}
printName();   // OrderService
```

### Example 2: Accidental global (and strict mode)
```js
function sloppy() {
  leaked = 100;      // no declaration: becomes global in sloppy mode
}
sloppy();
console.log(leaked);   // 100

(function () {
  "use strict";
  try {
    oops = 5;
  } catch (e) {
    console.log(e.name);   // ReferenceError
  }
})();
```

### Example 3: globalThis and module scope in Node.js
```js
var topLevel = "hello";
console.log(globalThis.topLevel);   // undefined in a Node module file

globalThis.appVersion = "1.0.0";    // deliberately global
console.log(appVersion);            // 1.0.0
```

## 5. Assignments
1. Create three functions that all read one global constant `TAX_RATE` and calculate tax for different amounts.
2. Create an accidental global in a function, print it outside, then fix it with `let` and show strict mode catching the mistake.
3. In Node, check whether `var x = 1;` at the top of a file appears on `globalThis`. Explain what you see.
4. List four reasons global variables are risky in a team project, and show one alternative (module export/import).

## 6. MCQs
**Q1.** A global variable is declared:
- A) Inside a function
- B) Outside all functions and blocks
- C) Inside an `if` block
- D) Only with `global`

**Q2.** In strict mode, assigning to an undeclared variable:
- A) Creates a global
- B) Creates a local
- C) Throws a `ReferenceError`
- D) Returns `undefined`

**Q3.** The universal way to access the global object is:
- A) `window`
- B) `global`
- C) `globalThis`
- D) `root`

**Q4.** In a Node.js file, a top-level `var` is:
- A) Always a property of `globalThis`
- B) Scoped to the module file
- C) Shared across all files
- D) Not allowed

### Answer Key
- Q1: **B**.
- Q2: **C**.
- Q3: **C**. `window` is browser only, `global` is Node only.
- Q4: **B**. Node wraps each file in a module scope.
