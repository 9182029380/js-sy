# Class 41: JavaScript Boolean

## 1. Definition
A **Boolean** is a primitive type with exactly two values: `true` and `false`. It represents a yes/no or on/off state and drives all decisions in code.

## 2. Usage
- Conditions in `if`, loops and ternaries.
- Flags such as `isActive`, `isAdmin`, `hasPaid`, `emailVerified`.
- Results of comparisons and validations.
- Feature toggles and permission checks in backend services.

## 3. Description
- Comparisons and logical operators produce booleans: `5 > 3`, `a && b`, `!x`.
- **Truthy and falsy**: any value is treated as true or false in a condition.
  - **Falsy (the complete list of 8 values)**: `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`. Everything else is truthy.
  - **Truthy**: everything else, including `"0"`, `"false"`, `[]`, `{}` and non-zero numbers.
- **Convert**: `Boolean(value)` or the double-not `!!value`.
- **Never** use `new Boolean(false)`. It creates an object, and objects are always truthy.
- **Logical operators**:
  - `&&` returns the first falsy value, or the last value.
  - `||` returns the first truthy value, or the last value.
  - `!` flips the value.
  - `??` returns the right side only when the left is `null` or `undefined`.
- Naming: start boolean names with `is`, `has`, `can` or `should`.

## 4. Examples

### Example 1: Comparisons and logic
```js
const age = 22, hasLicense = true;
console.log(age >= 18);                 // true
console.log(age >= 18 && hasLicense);   // true
console.log(!hasLicense);               // false
const isAdult = age >= 18;
if (isAdult) console.log("Adult");
```

### Example 2: Truthy and falsy
```js
const values = [0, "", null, undefined, NaN, "0", "false", [], {}, 42];
for (const v of values) {
  console.log(JSON.stringify(v), "->", Boolean(v));
}
console.log(!!"hello", !!0);   // true false
```

### Example 3: Short-circuit and the `new Boolean` trap
```js
const name = "";
console.log(name || "Anonymous");    // Anonymous
const user = { name: "Ravi" };
console.log(user && user.name);      // Ravi
console.log(0 ?? "default");         // 0

const obj = new Boolean(false);
console.log(obj ? "truthy" : "falsy");   // truthy (it's an object!)
console.log(typeof obj, typeof false);   // object boolean
```

## 5. Assignments
1. Write `canAccess(user)` returning `true` only when the user is active, verified and has role `"admin"` or `"manager"`.
2. Test the truthiness of 10 different values and record the results in a table. Explain which ones surprised you.
3. Write a function `isEmpty(value)` that returns `true` for `null`, `undefined`, `""`, `[]` and `{}`, and `false` otherwise. Do not treat `0` or `false` as empty.
4. Use `||`, `&&` and `??` to set default values for `username`, `port` (where 0 is valid) and a nested `config.db.host`. Explain your choice of operator each time.

## 6. MCQs
**Q1.** Which value is falsy?
- A) `"0"`
- B) `[]`
- C) `0`
- D) `{}`

**Q2.** What does `!!"hello"` return?
- A) `"hello"`
- B) `false`
- C) `true`
- D) `undefined`

**Q3.** What does `Boolean("false")` return?
- A) `false`
- B) `true`
- C) `undefined`
- D) Error

**Q4.** What is `null || "default"`?
- A) `null`
- B) `"default"`
- C) `true`
- D) `false`

### Answer Key
- Q1: **C**.
- Q2: **C**.
- Q3: **B**. Any non-empty string is truthy.
- Q4: **B**.
