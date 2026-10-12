# Class 47: JavaScript setInterval()

## 1. Definition
`setInterval()` calls a function **repeatedly**, with a fixed delay (in milliseconds) between calls, until it is stopped with `clearInterval()`.

Syntax: `const id = setInterval(callback, delay, arg1, arg2, ...)`

## 2. Usage
- Polling an API or database for changes.
- Health checks and heartbeat signals in services.
- Periodic cleanup (expired sessions, temp files, cache eviction).
- Countdowns, clocks and progress displays.
- Sending periodic metrics or logs.

## 3. Description
- Runs the callback every `delay` ms **until cleared**. Always keep the id and call `clearInterval(id)` when done, otherwise it runs forever and keeps a Node.js process alive.
- Like `setTimeout`, the delay is a **minimum**. If the callback takes longer than the interval, runs can bunch up or drift.
- **Drift problem**: for tasks that must not overlap (for example an async network call), prefer a **recursive `setTimeout`**, which schedules the next run only after the current one finishes.
- In Node.js, `interval.unref()` lets the process exit even if the interval is still active (useful for background housekeeping).
- Not suitable for exact timing. Use `Date.now()` for real elapsed time.
- Cron-style schedules in backends are usually handled with libraries like `node-cron`, or by the platform scheduler.

| | `setTimeout` | `setInterval` |
|---|---|---|
| Runs | Once | Repeatedly |
| Stop with | `clearTimeout` | `clearInterval` |
| Typical use | Delay, retry | Polling, heartbeat |

## 4. Examples

### Example 1: Run a few times, then stop
```js
let count = 0;
const id = setInterval(() => {
  count++;
  console.log("Tick", count);
  if (count === 3) {
    clearInterval(id);
    console.log("Stopped");
  }
}, 500);
```

### Example 2: Countdown
```js
let seconds = 5;
const timer = setInterval(() => {
  console.log(seconds);
  seconds--;
  if (seconds < 0) {
    clearInterval(timer);
    console.log("Go!");
  }
}, 1000);
```

### Example 3: Safe polling with recursive setTimeout
```js
const sleep = (ms) => new Promise((r) => setTimeout(r, ms));
let attempts = 0;
async function checkStatus() {
  attempts++;
  await sleep(100);               // pretend this is a network call
  return attempts >= 3 ? "ready" : "pending";
}

async function poll() {
  const status = await checkStatus();
  console.log("Status:", status);
  if (status !== "ready") setTimeout(poll, 200);   // next run only after this one finished
}
poll();

// Background housekeeping that doesn't block shutdown
const cleanup = setInterval(() => console.log("cleaning cache"), 60_000);
cleanup.unref();
```

## 5. Assignments
1. Print the current time every second for 5 seconds, then stop the interval.
2. Build a countdown timer that starts from a given number of seconds and prints `Time up!` at zero.
3. Write `poll(fn, intervalMs, maxAttempts)` that calls `fn` repeatedly until it returns true or attempts are used up, using recursive `setTimeout`.
4. Explain with a small experiment why `setInterval` with an async callback that takes longer than the interval can overlap, and fix it.

## 6. MCQs
**Q1.** `setInterval` runs a callback:
- A) Once
- B) Repeatedly until cleared
- C) Never
- D) Only when the user clicks

**Q2.** How do you stop an interval?
- A) `stopInterval(id)`
- B) `clearTimeout(id)` only
- C) `clearInterval(id)`
- D) `interval.delete()`

**Q3.** What happens if you never clear an interval in a Node.js script?
- A) The process may keep running
- B) Node throws an error
- C) It stops after 10 runs
- D) It runs once

**Q4.** For async tasks that must not overlap, a better pattern is:
- A) A very short `setInterval`
- B) Recursive `setTimeout`
- C) `while(true)`
- D) `setImmediate` only

### Answer Key
- Q1: **B**.
- Q2: **C**.
- Q3: **A**. An active interval keeps the Node.js event loop alive.
- Q4: **B**.
