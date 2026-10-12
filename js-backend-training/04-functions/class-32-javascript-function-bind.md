# Class 32: JavaScript Function - bind()

## 1. Definition
`bind()` is a function method that returns a **new function** with a permanently fixed `this` value and, optionally, some pre-filled arguments. It does **not** call the function immediately.

Syntax: `const newFn = func.bind(thisArg, arg1, arg2, ...)`

## 2. Usage
- Keeping the correct `this` when passing methods as callbacks (event handlers, timers, class methods).
- **Partial application**: creating specialised versions of a function.
- Reusing a function with the same `this` many times.

## 3. Description
- Returns a **bound function**. You call it later.
- The bound `this` **cannot be changed** afterwards, not even with `call()` or `apply()`.
- Extra arguments given to `bind()` are placed **first**. Arguments passed on later calls follow.
- Common problem solved: a method loses `this` when passed as a callback (`setTimeout(obj.method, 100)`).
- Arrow functions already keep `this` from where they are defined, so they do not need `bind()`.

| | Runs now? | Arguments | Returns |
|---|---|---|---|
| `call` | Yes | one by one | function's result |
| `apply` | Yes | array | function's result |
| `bind` | **No** | one by one (partial) | new function |

## 4. Examples

### Example 1: Losing and fixing `this`
```js
const user = {
  name: "Anil",
  greet() { return `Hi, I am ${this.name}`; }
};

const lost = user.greet;
try {
  console.log(lost());          // this is not user: name is undefined
} catch (e) {
  console.log(e.name);
}

const fixed = user.greet.bind(user);
console.log(fixed());           // Hi, I am Anil
```

### Example 2: Partial application
```js
function multiply(a, b) { return a * b; }

const double = multiply.bind(null, 2);
const triple = multiply.bind(null, 3);
console.log(double(10));   // 20
console.log(triple(10));   // 30
```

### Example 3: Callbacks and timers
```js
const counter = {
  count: 0,
  increment() {
    this.count++;
    console.log("Count:", this.count);
  }
};
setTimeout(counter.increment.bind(counter), 100);   // Count: 1

const bound = counter.increment.bind(counter);
bound.call({ count: 999 });   // still uses counter (this cannot be changed): Count: 2
```

## 5. Assignments
1. Create an object with a method that uses `this`. Pass the method to `setTimeout` first unbound (observe the problem), then with `bind()`.
2. Create `add10 = add.bind(null, 10)` and `add100` from a two-argument `add` function. Test both.
3. Build a `logger(level, message)` function and create `info` and `error` variants using `bind()` with the level pre-filled.
4. Explain with code why `bind()` is not needed for arrow functions inside a class method.

## 6. MCQs
**Q1.** What does `bind()` return?
- A) The result of the function
- B) A new function with `this` fixed
- C) `undefined`
- D) A Promise

**Q2.** After binding, can `call()` change the `this`?
- A) Yes
- B) No
- C) Only in strict mode
- D) Only for arrow functions

**Q3.** `const f = multiply.bind(null, 2); f(5)` where `multiply = (a, b) => a * b` gives:
- A) 7
- B) 10
- C) 2
- D) `NaN`

**Q4.** Which statement is true?
- A) `bind()` calls the function immediately
- B) `bind()` is only for arrays
- C) `bind()` is helpful for fixing `this` in callbacks
- D) `bind()` removes `this`

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **B**. `2 * 5 = 10`.
- Q4: **C**.
