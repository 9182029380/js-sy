# Class 05: Hello World Program in JavaScript

## 1. Definition
A **Hello World program** is the simplest program that prints a message. In JavaScript it is written with `console.log()` and run with Node.js (or inside a browser).

## 2. Usage
- Verify that Node.js is installed and working.
- Confirm your editor, terminal and file setup.
- Starting point for every new script, microservice or learning exercise.

## 3. Description
Ways to print output:

| Method | Where | Notes |
|---|---|---|
| `console.log()` | Node and browser | Most common, adds a newline |
| `console.error()` | Node and browser | Writes to the error stream (stderr in Node) |
| `process.stdout.write()` | Node only | No automatic newline |
| `alert()` | Browser only | Popup, not available in Node |
| `document.write()` | Browser only | Avoid in real code |

Steps in Node.js:
1. Create `hello.js`.
2. Write the code.
3. Open a terminal in that folder and run `node hello.js`.

## 4. Examples

### Example 1: Basic Hello World
```js
console.log("Hello, World!");
```
**Output**: `Hello, World!`

### Example 2: Using variables and template literals
```js
const course = "JavaScript Backend";
const day = 1;
console.log(`Welcome to ${course}, Day ${day}`);
```
**Output**: `Welcome to JavaScript Backend, Day 1`

### Example 3: stdout, stderr and multiple lines
```js
process.stdout.write("Loading");
process.stdout.write("...\n");
console.error("This goes to stderr");
console.log("Line 1\nLine 2");
```
Use `console.error` for errors in servers so logs can be separated from normal output.

## 5. Assignments
1. Create `hello.js` printing `Hello, World!` and run it from the terminal. Take a screenshot of the output.
2. Print your full name, company and trainer name on three lines using a single `console.log` call and `\n`.
3. Write a program that prints a 5-line banner made of `*` characters using `console.log` (one call per line).
4. Using `process.stdout.write`, print `1 2 3 4 5` on one line, then a newline at the end.

## 6. MCQs
**Q1.** Which prints to the console in both Node.js and the browser?
- A) `alert()`
- B) `console.log()`
- C) `document.write()`
- D) `print()`

**Q2.** Which command runs `hello.js`?
- A) `npm hello.js`
- B) `js hello.js`
- C) `node hello.js`
- D) `run hello`

**Q3.** `\n` inside a string means:
- A) Tab
- B) New line
- C) Backslash
- D) Space

**Q4.** `console.error()` writes to:
- A) stdout
- B) stderr
- C) A file
- D) The browser alert box

### Answer Key
- Q1: **B**.
- Q2: **C**.
- Q3: **B**.
- Q4: **B**. Error output goes to the standard error stream.
