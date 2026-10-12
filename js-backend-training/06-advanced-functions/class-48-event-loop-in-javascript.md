# Class 48: Event Loop in JavaScript

## 1. Definition
The **event loop** is the mechanism that lets single-threaded JavaScript handle **asynchronous** work. It continuously checks whether the **call stack** is empty and, when it is, moves the next ready task from a queue onto the stack.

## 2. Usage
- Understanding why Node.js can serve thousands of connections with one thread.
- Predicting the order of output from `setTimeout`, Promises and `async/await`.
- Avoiding **blocking** code (heavy loops, sync file reads) that freezes the whole server.
- Debugging slow APIs and timing bugs.
- Core interview topic for Node.js roles.

## 3. Description
Main parts:

| Part | Role |
|---|---|
| **Call stack** | Where synchronous code runs, one function at a time (LIFO) |
| **Web / Node APIs** | Timers, I/O, network. Work happens outside the stack (browser APIs, or libuv in Node.js) |
| **Macrotask queue** | Timer callbacks (`setTimeout`, `setInterval`), I/O callbacks, `setImmediate` |
| **Microtask queue** | Promise callbacks (`.then`, `.catch`, `.finally`), `await` continuations, `queueMicrotask`, `process.nextTick` (Node, runs before promise microtasks) |
| **Event loop** | Picks the next task when the stack is empty |

Order of execution:
1. Run all **synchronous** code on the call stack.
2. When the stack is empty, run **all microtasks** (including new ones added meanwhile).
3. Take **one macrotask**, run it, then run all microtasks again.
4. Repeat.

Node.js event loop phases (libuv), in order: **timers**, pending callbacks, idle/prepare, **poll** (I/O), **check** (`setImmediate`), close callbacks. Between each phase, `process.nextTick` and promise microtasks are drained.

Key facts:
- JavaScript runs one thing at a time. Long synchronous work **blocks everything**.
- `await` pauses only the async function, not the whole program: its continuation becomes a microtask.
- For CPU-heavy work in Node.js, use **worker threads** or a separate service.
- `setTimeout(fn, 0)` runs after all pending microtasks.

## 4. Examples

### Example 1: Basic ordering
```js
console.log("1: sync start");
setTimeout(() => console.log("4: timeout (macrotask)"), 0);
Promise.resolve().then(() => console.log("3: promise (microtask)"));
console.log("2: sync end");
// 1, 2, 3, 4
```

### Example 2: async/await and nextTick
```js
async function demo() {
  console.log("A: inside async (sync part)");
  await null;                                  // rest becomes a microtask
  console.log("D: after await");
}
console.log("start");
demo();
process.nextTick(() => console.log("C: nextTick"));
Promise.resolve().then(() => console.log("E: then"));
console.log("B: end of main script");
// start, A, B, C (nextTick first), D, E
```

### Example 3: Blocking vs non-blocking
```js
setTimeout(() => console.log("timer fired"), 100);

const start = Date.now();
while (Date.now() - start < 300) { /* blocks the event loop for 300 ms */ }
console.log("blocking loop done after", Date.now() - start, "ms");
// The 100 ms timer only fires AFTER the blocking loop finishes.

const fs = require("node:fs");
fs.readFile(__filename, () => {
  setTimeout(() => console.log("timeout"), 0);
  setImmediate(() => console.log("immediate"));   // inside I/O: immediate runs first
});
```

## 5. Assignments
1. Predict, then run, the output of a script with two `setTimeout` calls (0 ms and 10 ms), two Promise `.then` calls and three synchronous logs. Draw the call stack and queues on paper for the first example.
2. Demonstrate how a heavy synchronous loop delays a `setTimeout`. Then show how splitting the loop into chunks with `setImmediate` keeps the timer responsive.
3. Explain the difference between `process.nextTick`, `Promise.then`, `setImmediate` and `setTimeout(fn, 0)` with a script that shows their order.
4. Write an async function that fetches (simulated) three items **sequentially** with `await` in a loop, then **in parallel** with `Promise.all`. Measure both times and explain the difference.

## 6. MCQs
**Q1.** The event loop moves a queued task to the call stack when:
- A) The stack is empty
- B) A timer starts
- C) The file is saved
- D) Memory is full

**Q2.** Which runs first?
- A) `setTimeout(fn, 0)` callback
- B) A resolved Promise `.then` callback
- C) `setInterval` callback
- D) They run at the same time

**Q3.** What happens if you run a long synchronous loop in a Node.js server?
- A) Other requests are processed in parallel
- B) All requests wait until the loop ends
- C) Node.js creates a new thread automatically
- D) The loop is skipped

**Q4.** What is the output order? `console.log("A"); setTimeout(()=>console.log("B"),0); Promise.resolve().then(()=>console.log("C")); console.log("D");`
- A) A B C D
- B) A D B C
- C) A D C B
- D) D A C B

### Answer Key
- Q1: **A**.
- Q2: **B**. Microtasks (Promises) run before the next macrotask (timers).
- Q3: **B**. JavaScript is single-threaded, so the whole event loop is blocked.
- Q4: **C**. Sync: A, D. Microtask: C. Macrotask: B.
