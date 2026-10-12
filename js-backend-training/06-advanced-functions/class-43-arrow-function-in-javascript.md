# Class 43: Arrow Function in JavaScript

## 1. Definition
An **arrow function** (ES6) is a shorter syntax for writing function expressions using `=>`. It does not have its own `this`, `arguments` or `super`: it uses those of the surrounding scope.

## 2. Usage
- Short callbacks for `map`, `filter`, `reduce`, `forEach`, `sort`.
- Promise chains and `async` helpers.
- Keeping `this` from the enclosing scope inside timers and class methods.
- Concise utility functions and middleware.

## 3. Description
Syntax forms:
```js
const f1 = (a, b) => { return a + b; };   // block body
const f2 = (a, b) => a + b;               // implicit return
const f3 = a => a * 2;                    // one parameter, parentheses optional
const f4 = () => "hi";                    // no parameters
const f5 = () => ({ ok: true });          // returning an object literal: wrap in ()
```
Differences from regular functions:
- **Lexical `this`**: takes `this` from where it is defined. `call`, `apply` and `bind` cannot change it.
- **No `arguments` object**: use rest parameters `(...args)`.
- **Cannot be used as constructors** (`new` throws).
- **Not hoisted** like declarations.
- No `prototype` property.

When **not** to use: object methods that need their own `this`, constructors, and when a name is needed for clear stack traces or recursion (use a normal function).

## 4. Examples

### Example 1: Syntax shortcuts
```js
const add = (a, b) => a + b;
const square = n => n * n;
const hello = () => "Hello!";
const makeUser = (name) => ({ name, active: true });
console.log(add(2, 3), square(4), hello(), makeUser("Anil"));
```

### Example 2: With array methods
```js
const prices = [100, 250, 400, 80];
const result = prices
  .filter(p => p > 90)
  .map(p => p * 1.18)
  .reduce((sum, p) => sum + p, 0);
console.log(result.toFixed(2));   // 885.40
```

### Example 3: Lexical this
```js
const timer = {
  seconds: 0,
  startRegular() {
    setTimeout(function () {
      console.log("Regular:", this.seconds);   // this is NOT timer (undefined)
    }, 0);
  },
  startArrow() {
    setTimeout(() => {
      console.log("Arrow:", this.seconds);     // this is timer (0)
    }, 0);
  }
};
timer.startRegular();
timer.startArrow();

const obj = { name: "X", greet: () => this === undefined || this === module.exports };
console.log(obj.greet());   // arrow does not get obj as this
```

## 5. Assignments
1. Convert five regular functions you wrote earlier into arrow functions.
2. Use arrow functions with `map`, `filter` and `reduce` to get the total price of the in-stock items from an array of product objects.
3. Show with code why an arrow function should not be used as an object method that depends on `this`.
4. Write a `compose(f, g)` function that returns `x => f(g(x))` and use it to combine two small arrow functions.

## 6. MCQs
**Q1.** Which is a valid arrow function?
- A) `x => x * 2`
- B) `function => x * 2`
- C) `=> x * 2`
- D) `x -> x * 2`

**Q2.** Arrow functions get `this` from:
- A) The caller
- B) The enclosing (lexical) scope
- C) `globalThis` always
- D) They have no `this` and cannot use it

**Q3.** How do you return an object literal directly from an arrow function?
- A) `() => { a: 1 }`
- B) `() => ({ a: 1 })`
- C) `() => [a: 1]`
- D) `() => return { a: 1 }`

**Q4.** Can you use `new` on an arrow function?
- A) Yes
- B) No, it throws a `TypeError`
- C) Only with parameters
- D) Only in strict mode

### Answer Key
- Q1: **A**.
- Q2: **B**.
- Q3: **B**.
- Q4: **B**.
