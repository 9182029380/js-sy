# Class 03: JavaScript Versions

## 1. Definition
JavaScript is standardised as **ECMAScript (ES)** by ECMA International (specification ECMA-262). A **JavaScript version** means an ECMAScript edition, such as ES5, ES6 (ES2015) or ES2024. Engines like V8 implement these editions.

## 2. Usage
- Decide which syntax is safe on your Node.js version.
- Read modern codebases that use `async/await`, optional chaining and modules.
- Maintain legacy code written in ES5 style (`var`, `function`, callbacks).
- Configure tools like Babel, TypeScript and ESLint with the correct target.

## 3. Description
Since **ES2015**, a new edition is released every year (June). Features go through proposal stages before being added.

| Edition | Year | Notable additions |
|---|---|---|
| ES1 to ES3 | 1997 to 1999 | Core language, regular expressions, try/catch |
| ES5 | 2009 | `strict mode`, JSON support, `forEach`, `map`, `filter` |
| **ES6 / ES2015** | 2015 | `let`, `const`, arrow functions, classes, template literals, destructuring, Promises, modules |
| ES2016 | 2016 | `**` operator, `Array.includes` |
| ES2017 | 2017 | `async/await`, `Object.entries`, `Object.values` |
| ES2018 | 2018 | Object spread and rest, `Promise.finally` |
| ES2019 | 2019 | `flat`, `flatMap`, `Object.fromEntries` |
| ES2020 | 2020 | `BigInt`, optional chaining `?.`, nullish coalescing `??` |
| ES2021 | 2021 | `replaceAll`, logical assignment `??=` |
| ES2022 | 2022 | Top-level `await`, class fields, `Array.at()` |
| ES2023 | 2023 | `toSorted`, `toReversed`, `findLast` |
| ES2024 | 2024 | `Object.groupBy`, `Promise.withResolvers` |
| ES2025 | 2025 | Set methods (`union`, `intersection`), iterator helpers |

Node.js supports modern editions. Always check the Node version your project targets with `node --version`.

## 4. Examples

### Example 1: ES5 vs ES6 style
```js
// ES5
var add5 = function (a, b) { return a + b; };
var msg5 = "Total: " + add5(2, 3);

// ES6+
const add = (a, b) => a + b;
const msg = `Total: ${add(2, 3)}`;
console.log(msg5, msg);
```

### Example 2: ES2020 optional chaining and nullish coalescing
```js
const user = { profile: { city: "Hyderabad" } };
console.log(user.profile?.city);          // Hyderabad
console.log(user.address?.street);        // undefined (no error)
console.log(user.address?.street ?? "N/A"); // N/A
```

### Example 3: ES2023 and ES2024 helpers
```js
const nums = [3, 1, 2];
const sorted = nums.toSorted();      // new array, original unchanged
console.log(sorted, nums);           // [1,2,3] [3,1,2]

const orders = [
  { id: 1, status: "paid" },
  { id: 2, status: "pending" },
  { id: 3, status: "paid" }
];
console.log(Object.groupBy(orders, o => o.status));
```

## 5. Assignments
1. Run `node --version` and `process.versions.v8`. Note them down, then list three features from the table that your Node version supports. Prove each with a small snippet.
2. Rewrite this ES5 code in modern JS: `var total = 0; var nums = [1,2,3]; for (var i = 0; i < nums.length; i++) { total = total + nums[i]; } console.log("Total is " + total);`
3. Use `?.` and `??` to safely read `order.customer.address.pincode` from an object that may be missing parts, defaulting to `"000000"`.
4. Create a table of the ES version in which each of these arrived: `let`, `async/await`, `BigInt`, `Array.at()`. Verify your answers using a trusted source.

## 6. MCQs
**Q1.** ES6 is also known as:
- A) ES2006
- B) ES2015
- C) ES2020
- D) ES5.1

**Q2.** Which feature arrived in ES2017?
- A) `async/await`
- B) Optional chaining
- C) `let`
- D) `BigInt`

**Q3.** What does `user?.address?.city` do if `address` is undefined?
- A) Throws a TypeError
- B) Returns `null`
- C) Returns `undefined`
- D) Returns an empty string

**Q4.** The body that standardises JavaScript is:
- A) W3C
- B) ECMA International
- C) Oracle
- D) Mozilla

### Answer Key
- Q1: **B**.
- Q2: **A**. `let` is ES6, optional chaining and BigInt are ES2020.
- Q3: **C**. Optional chaining short-circuits to `undefined`.
- Q4: **B**. ECMA-262 is the specification.
