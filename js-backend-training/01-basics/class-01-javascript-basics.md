# Class 01: JavaScript Basics

## 1. Definition
**JavaScript (JS)** is a high-level, dynamically typed, multi-paradigm programming language. It started as a browser scripting language and, with **Node.js**, now runs on servers, in command-line tools and in serverless functions.

## 2. Usage
- **Backend APIs**: REST and GraphQL servers with Node.js (Express, NestJS, Fastify).
- **Automation and CLI tools**: build scripts, file processing, DevOps utilities.
- **Microservices and serverless**: AWS Lambda, Azure Functions, Google Cloud Functions.
- **Frontend**: Angular, React, Vue (the same language on both sides of the stack).
- **Real-time apps**: chat, notifications, streaming via WebSockets.

## 3. Description
- JavaScript code is executed by an **engine**. Chrome and Node.js use **V8**; Firefox uses SpiderMonkey; Safari uses JavaScriptCore.
- **Node.js** = V8 engine + a runtime that adds file system, networking, processes and more. It is not a language, it is a runtime for JavaScript.
- A JS program is a sequence of **statements** executed top to bottom.
- JavaScript is **single-threaded** (one call stack) but handles I/O without blocking through an event loop (covered in Class 48).
- Run a file with `node filename.js`. Try short snippets in the REPL by typing `node`.

## 4. Examples

### Example 1: Printing output
```js
console.log("Welcome to JS backend training");
console.log(10 + 5);
console.log("Total:", 10 + 5);
```
**Output**
```
Welcome to JS backend training
15
Total: 15
```

### Example 2: Dynamic typing
```js
let data = 42;
console.log(typeof data);   // number
data = "forty-two";
console.log(typeof data);   // string
data = { id: 42 };
console.log(typeof data);   // object
```
A variable can hold a different type at different times. No type is declared.

### Example 3: Reading command-line input in Node.js
```js
// save as greet.js and run: node greet.js Sharath
const name = process.argv[2] || "Guest";
console.log(`Hello, ${name}!`);
```
`process.argv` is a Node.js array of command-line arguments. It is a backend feature that does not exist in a browser.

## 5. Assignments
1. Install Node.js, run `node --version` and `node` (REPL). In the REPL, calculate `(25 * 4) + 10` and note the result.
2. Create `intro.js` that prints your name, role and city on three separate lines using `console.log`.
3. Write a script that prints `typeof` for these values: `100`, `"100"`, `true`, `undefined`, `null`, `[]`, `{}`. Explain any result that surprises you.
4. Write `add.js` that takes two numbers from the command line (`node add.js 4 6`) and prints their sum. Hint: arguments arrive as strings, convert with `Number()`.

## 6. MCQs
**Q1.** Which engine runs JavaScript inside Node.js?
- A) SpiderMonkey
- B) V8
- C) Chakra
- D) JVM

**Q2.** Which statement about Node.js is correct?
- A) It is a new programming language
- B) It is a runtime that executes JavaScript outside the browser
- C) It can only be used for frontend work
- D) It requires Java to be installed

**Q3.** What does `typeof 42` return?
- A) `"int"`
- B) `"integer"`
- C) `"number"`
- D) `"digit"`

**Q4.** How do you run `app.js` with Node.js?
- A) `run app.js`
- B) `js app.js`
- C) `node app.js`
- D) `npm app.js`

### Answer Key
- Q1: **B**. V8 is the engine used by Chrome and Node.js.
- Q2: **B**. Node.js is a runtime, not a language.
- Q3: **C**. JS has a single `number` type for integers and decimals.
- Q4: **C**. `node app.js` runs the file.
