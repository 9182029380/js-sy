# Class 46: JavaScript setTimeout()

## 1. Definition
`setTimeout()` schedules a function to run **once** after a minimum delay (in milliseconds). It returns a **timer id** that can be used to cancel it with `clearTimeout()`.

Syntax: `const id = setTimeout(callback, delay, arg1, arg2, ...)`

## 2. Usage
- Delaying an action (show a message, retry later).
- **Retry with backoff** after a failed request.
- **Debounce**: wait until the user stops typing or events stop firing.
- Simulating async work in demos and tests.
- Request **timeouts**: give up if something takes too long.
- Deferring heavy work so the event loop can breathe (`setTimeout(fn, 0)`).

## 3. Description
- The delay is a **minimum**, not a guarantee. The callback runs after the delay **and** only when the call stack is free.
- `setTimeout(fn, 0)` means "run as soon as the current code finishes", not "now".
- Extra arguments after the delay are passed to the callback.
- Pass the function **reference**, not a call: `setTimeout(sayHi, 1000)`.
- `clearTimeout(id)` cancels a pending timer.
- In **Node.js** the returned value is a `Timeout` object (in browsers it is a number). Methods: `.unref()` lets the process exit even if the timer is pending, `.ref()`, `.refresh()`.
- Use a Promise wrapper for `async/await` code: `const sleep = (ms) => new Promise(r => setTimeout(r, ms));`. Node also offers `require("node:timers/promises").setTimeout(ms)`.
- Order of execution: synchronous code first, then promise callbacks (microtasks), then timer callbacks (macrotasks).

## 4. Examples

### Example 1: Basic delay and arguments
```js
console.log("Start");
setTimeout(() => console.log("After 1 second"), 1000);
setTimeout((name, city) => console.log(`${name} from ${city}`), 500, "Anil", "Hyderabad");
console.log("End");
// Start, End, Anil from Hyderabad, After 1 second
```

### Example 2: Cancel a timer and use a sleep helper
```js
const id = setTimeout(() => console.log("This never runs"), 1000);
clearTimeout(id);

const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));
(async () => {
  console.log("Working...");
  await sleep(300);
  console.log("Done after 300 ms");
})();
```

### Example 3: Zero delay ordering, timeout and debounce
```js
setTimeout(() => console.log("timeout 0"), 0);
Promise.resolve().then(() => console.log("promise"));
console.log("sync");
// sync, promise, timeout 0

function debounce(fn, wait) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), wait);
  };
}
const save = debounce((text) => console.log("Saved:", text), 200);
save("a"); save("ab"); save("abc");   // only "Saved: abc" prints
```

## 5. Assignments
1. Print `Hello` after 2 seconds, then print `World` 1 second after that using two `setTimeout` calls (nested or with a sleep helper).
2. Write `withTimeout(promise, ms)` that rejects with `"Timeout"` if the promise does not settle in time (use `Promise.race`).
3. Predict, then run, the output order of a script mixing synchronous logs, `setTimeout(..., 0)` and `Promise.resolve().then(...)`. Explain the order.
4. Implement a retry function that waits 100 ms, 200 ms, then 400 ms between three attempts of an operation that fails the first two times.

## 6. MCQs
**Q1.** `setTimeout` runs the callback:
- A) Repeatedly
- B) Once after a delay
- C) Immediately
- D) Never

**Q2.** What does `clearTimeout(id)` do?
- A) Pauses all timers
- B) Cancels the pending timer
- C) Runs the callback now
- D) Deletes the callback function

**Q3.** `setTimeout(fn, 0)` means:
- A) `fn` runs synchronously
- B) `fn` runs after the current synchronous code and microtasks
- C) `fn` never runs
- D) `fn` runs before promises

**Q4.** In which order do these print? `setTimeout(()=>console.log("T"),0); Promise.resolve().then(()=>console.log("P")); console.log("S");`
- A) T, P, S
- B) S, T, P
- C) S, P, T
- D) P, S, T

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **B**.
- Q4: **C**. Synchronous first, then microtasks (promises), then timers.
