# Class 34: JavaScript Arrays

## 1. Definition
An **array** is an ordered, zero-indexed collection of values. It can hold any mix of types and grows or shrinks dynamically.

## 2. Usage
- Lists of records returned from a database or API (users, orders, logs).
- Queues, stacks, batches and pagination results.
- Storing multiple values under one name.
- Data pipelines with `map`, `filter` and `reduce`.

## 3. Description
Creating arrays:
```js
const a = [10, 20, 30];          // literal (preferred)
const b = new Array(3);          // 3 empty slots
const c = Array.from("abc");     // ['a','b','c']
const d = Array.of(7);           // [7]
```
Basics:
- **Index** starts at `0`. `arr[0]` is the first item, `arr[arr.length - 1]` the last (or `arr.at(-1)`).
- `length` gives the number of items and can be changed.
- Arrays are objects: `typeof [] === "object"`. Check with `Array.isArray(x)`.
- Arrays are **reference types** (copying a variable shares the array).
- Copy: `[...arr]` (shallow) or `structuredClone(arr)` (deep).
- Destructuring: `const [first, second] = arr;`
- **Nested arrays** (2D): `matrix[row][col]`.
- Iterate with `for`, `for...of`, `forEach` or array methods (next class).

## 4. Examples

### Example 1: Create, access and modify
```js
const fruits = ["apple", "banana", "cherry"];
console.log(fruits[0], fruits.at(-1), fruits.length);   // apple cherry 3
fruits[1] = "mango";
fruits[3] = "grape";
console.log(fruits);   // [ 'apple', 'mango', 'cherry', 'grape' ]
```

### Example 2: Destructuring, spread and 2D arrays
```js
const [first, , third, ...rest] = [1, 2, 3, 4, 5];
console.log(first, third, rest);   // 1 3 [ 4, 5 ]

const a = [1, 2], b = [3, 4];
console.log([...a, ...b]);          // [ 1, 2, 3, 4 ]

const matrix = [[1, 2], [3, 4]];
console.log(matrix[1][0]);          // 3
```

### Example 3: Array of objects (typical API data)
```js
const users = [
  { id: 1, name: "Anil", active: true },
  { id: 2, name: "Ravi", active: false }
];
for (const u of users) console.log(u.id, u.name);
console.log(users.length, Array.isArray(users));   // 2 true
```

## 5. Assignments
1. Create an array of 5 numbers. Print the first, the last, the length and the sum.
2. Find the second largest number in an array without using `sort()`.
3. Given `[[1,2,3],[4,5,6]]`, print every element with nested loops, then compute the sum of each row.
4. Create an array of 4 product objects (`name`, `price`) and print the names of the products that cost more than 500.

## 6. MCQs
**Q1.** What is the index of the first element?
- A) 1
- B) 0
- C) -1
- D) Depends

**Q2.** What does `typeof []` return?
- A) `"array"`
- B) `"list"`
- C) `"object"`
- D) `"undefined"`

**Q3.** Which correctly checks that `x` is an array?
- A) `typeof x === "array"`
- B) `x instanceof Object`
- C) `Array.isArray(x)`
- D) `x.isArray()`

**Q4.** What is `[10, 20, 30].at(-1)`?
- A) 10
- B) 30
- C) `undefined`
- D) 20

### Answer Key
- Q1: **B**.
- Q2: **C**.
- Q3: **C**.
- Q4: **B**.
