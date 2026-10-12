# Class 11: JavaScript Data Types

## 1. Definition
A **data type** defines the kind of value a variable holds and what operations can be done on it. JavaScript has **primitive** types and **non-primitive (reference)** types.

## 2. Usage
- Validating API input (is this a number? a string? an array?).
- Preventing bugs from unexpected type conversion.
- Choosing the right structure: object for records, array for lists, `BigInt` for very large IDs, `Symbol` for unique keys.

## 3. Description

**Primitive types** (immutable, stored by value):

| Type | Example | Notes |
|---|---|---|
| `string` | `"hello"` | Text |
| `number` | `42`, `3.14`, `NaN`, `Infinity` | Integers and decimals (64-bit float) |
| `bigint` | `123n` | Integers beyond `Number.MAX_SAFE_INTEGER` |
| `boolean` | `true`, `false` | Logical |
| `undefined` | `undefined` | Declared but no value |
| `null` | `null` | Intentional "no value" |
| `symbol` | `Symbol("id")` | Unique identifier |

**Non-primitive types** (stored by reference): `object`, `array`, `function`, `Date`, `Map`, `Set` and more.

**Checking types**: `typeof value`. Quirks: `typeof null` is `"object"` (a historical bug) and `typeof []` is `"object"`. Use `Array.isArray()` for arrays.

**Falsy values**: `false`, `0`, `""`, `null`, `undefined`, `NaN`, `0n`. Everything else is truthy.

**Type conversion**: `Number("42")`, `String(42)`, `Boolean(0)`, `parseInt("42px")`.

## 4. Examples

### Example 1: Checking primitive types
```js
console.log(typeof "hi");        // string
console.log(typeof 42);          // number
console.log(typeof 10n);         // bigint
console.log(typeof true);        // boolean
console.log(typeof undefined);   // undefined
console.log(typeof null);        // object (known quirk)
console.log(typeof Symbol("a")); // symbol
```

### Example 2: Value vs reference
```js
let a = 10;
let b = a;
b = 20;
console.log(a, b);   // 10 20  (copied value)

const obj1 = { n: 1 };
const obj2 = obj1;
obj2.n = 99;
console.log(obj1.n); // 99  (same reference)
```

### Example 3: Number edge cases and conversion
```js
console.log(0.1 + 0.2);                 // 0.30000000000000004
console.log(Number.MAX_SAFE_INTEGER);   // 9007199254740991
console.log(9007199254740993n + 1n);    // 9007199254740994n
console.log(Number("abc"));             // NaN
console.log(Number("42"), parseInt("42px"));   // 42 42
console.log(Array.isArray([1, 2]));     // true
```

## 5. Assignments
1. Create one variable of every primitive type and print its `typeof`. Note which result surprised you.
2. Write a function `describe(value)` that returns `"array"`, `"null"` or the proper `typeof` result for any value.
3. Show how copying an object by assignment differs from copying a number. Then copy an object properly with spread `{...obj}`.
4. Explain why `0.1 + 0.2 !== 0.3`, and write code to compare them safely (hint: tolerance with `Math.abs`).

## 6. MCQs
**Q1.** What is `typeof null`?
- A) `"null"`
- B) `"undefined"`
- C) `"object"`
- D) `"number"`

**Q2.** Which is NOT a primitive type?
- A) `string`
- B) `symbol`
- C) `array`
- D) `bigint`

**Q3.** Which value is truthy?
- A) `0`
- B) `""`
- C) `"0"`
- D) `NaN`

**Q4.** What does `Number("abc")` return?
- A) `0`
- B) `undefined`
- C) `NaN`
- D) Throws an error

### Answer Key
- Q1: **C**. A long-standing quirk.
- Q2: **C**. Arrays are objects.
- Q3: **C**. A non-empty string is truthy, even `"0"`.
- Q4: **C**.
