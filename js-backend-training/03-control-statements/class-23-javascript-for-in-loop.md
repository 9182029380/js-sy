# Class 23: JavaScript for...in Loop

## 1. Definition
The **for...in loop** iterates over the **enumerable property keys** (names) of an object, including inherited enumerable properties.

## 2. Usage
- Looping over properties of a plain object (config, headers, query params).
- Debugging and inspecting objects.
- For most cases, `Object.keys()`, `Object.values()` and `Object.entries()` with `for...of` are safer.

## 3. Description
Syntax:
```js
for (const key in object) {
  // key is a string
  // object[key] is the value
}
```
- Gives **keys as strings**, even for arrays (`"0"`, `"1"`).
- Also visits **inherited** enumerable properties from the prototype chain. Use `Object.hasOwn(obj, key)` to filter own properties.
- **Do not use** `for...in` to loop over arrays: order and inherited keys are not guaranteed to behave as expected.
- Compare:

| | `for...in` | `for...of` |
|---|---|---|
| Gives | keys | values |
| Works on | objects (and arrays, not recommended) | iterables |
| Plain object | Yes | No |

## 4. Examples

### Example 1: Object keys and values
```js
const employee = { id: 7, name: "Kiran", dept: "Cloud" };
for (const key in employee) {
  console.log(`${key}: ${employee[key]}`);
}
```

### Example 2: Inherited properties and hasOwn
```js
const base = { role: "user" };
const admin = Object.create(base);
admin.name = "Root";

for (const key in admin) {
  console.log(key, Object.hasOwn(admin, key));
}
// name true
// role false   (inherited)
```

### Example 3: Why not arrays
```js
const arr = ["a", "b"];
arr.extra = "oops";
for (const k in arr) console.log(k);     // 0 1 extra
for (const v of arr) console.log(v);     // a b
```

## 5. Assignments
1. Create an object representing a product (5 properties) and print every key/value pair with `for...in`.
2. Count how many properties of an object have a numeric value.
3. Write a function `ownKeys(obj)` that returns only own keys using `for...in` and `Object.hasOwn`.
4. Show with code the difference between looping an array with `for...in` and `for...of`. Explain which one you would use and why.

## 6. MCQs
**Q1.** `for...in` provides:
- A) Values
- B) Keys as strings
- C) Indexes as numbers
- D) Entries as arrays

**Q2.** Which loop is recommended for arrays?
- A) `for...in`
- B) `for...of`
- C) `switch`
- D) `while(true)`

**Q3.** Does `for...in` include inherited enumerable properties?
- A) No
- B) Yes
- C) Only for arrays
- D) Only in strict mode

**Q4.** Which checks that a key belongs to the object itself?
- A) `Object.hasOwn(obj, key)`
- B) `key in obj`
- C) `typeof key`
- D) `obj.has(key)`

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **B**.
- Q4: **A**. `key in obj` also returns true for inherited keys.
