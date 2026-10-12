# Class 35: JavaScript Array Methods

## 1. Definition
**Array methods** are built-in functions on arrays that add, remove, search, transform, sort and combine items. They are the main tools for working with lists of data.

## 2. Usage
- Transforming API data (`map`), filtering records (`filter`), summing totals (`reduce`).
- Searching (`find`, `includes`, `some`, `every`).
- Managing queues and stacks (`push`, `pop`, `shift`, `unshift`).
- Sorting and grouping results for reports.

## 3. Description

**Mutating methods** (change the original array)

| Method | Purpose |
|---|---|
| `push(x)` / `pop()` | Add / remove at the end |
| `unshift(x)` / `shift()` | Add / remove at the start |
| `splice(start, deleteCount, ...items)` | Insert, remove, replace |
| `sort(compareFn)` | Sort in place |
| `reverse()` | Reverse in place |

**Non-mutating methods** (return new values)

| Method | Purpose |
|---|---|
| `map(fn)` | Transform each item into a new array |
| `filter(fn)` | Keep items where `fn` is true |
| `reduce(fn, initial)` | Combine into a single value |
| `find(fn)` / `findIndex(fn)` | First match / its index |
| `some(fn)` / `every(fn)` | Any / all match |
| `includes(x)` / `indexOf(x)` | Search by value |
| `slice(start, end)` | Copy a portion |
| `concat()`, `flat()`, `flatMap()` | Combine / flatten |
| `join(sep)` | Array to string |
| `forEach(fn)` | Run for each item (returns nothing) |
| `toSorted()`, `toReversed()`, `toSpliced()` | Non-mutating versions (ES2023) |

Important: `sort()` with no function sorts items as **strings**, so `[10, 9, 1].sort()` gives `[1, 10, 9]`. Always pass `(a, b) => a - b` for numbers.

## 4. Examples

### Example 1: Add, remove, slice and splice
```js
const list = [1, 2, 3];
list.push(4);            // [1,2,3,4]
list.unshift(0);         // [0,1,2,3,4]
list.pop();              // removes 4
list.shift();            // removes 0
console.log(list);       // [1,2,3]
console.log(list.slice(1, 3));   // [2,3] (original unchanged)
list.splice(1, 1, "x", "y");     // remove 1 item at index 1, insert two
console.log(list);       // [ 1, 'x', 'y', 3 ]
```

### Example 2: map, filter, reduce chain
```js
const orders = [
  { id: 1, amount: 500, paid: true },
  { id: 2, amount: 300, paid: false },
  { id: 3, amount: 900, paid: true }
];
const paidTotal = orders
  .filter((o) => o.paid)
  .map((o) => o.amount)
  .reduce((sum, a) => sum + a, 0);
console.log(paidTotal);   // 1400
```

### Example 3: Search, sort and check
```js
const nums = [10, 9, 1, 25];
console.log(nums.toSorted());                 // [ 1, 10, 25, 9 ] (string sort)
console.log(nums.toSorted((a, b) => a - b));  // [ 1, 9, 10, 25 ]

console.log(nums.find((n) => n > 9));         // 10
console.log(nums.some((n) => n > 20), nums.every((n) => n > 0));   // true true
console.log(nums.includes(25), nums.indexOf(1));   // true 2
console.log(["a", "b", "c"].join("-"));       // a-b-c
```

## 5. Assignments
1. From `[1,2,3,4,5,6,7,8,9,10]`, create an array of squares of only the odd numbers using `filter` and `map`.
2. Given an array of employee objects with `salary`, calculate the total and average salary with `reduce`.
3. Sort an array of products by price ascending, then by name alphabetically (use `localeCompare`). Print the result.
4. Remove duplicates from `[1,2,2,3,3,3,4]` in two ways: with `Set` and with `filter` + `indexOf`.

## 6. MCQs
**Q1.** Which method adds an item to the end of an array?
- A) `unshift`
- B) `push`
- C) `shift`
- D) `concat` (mutating)

**Q2.** `[1,2,3].map(x => x * 2)` returns:
- A) `[1,2,3]`
- B) `[2,4,6]`
- C) `12`
- D) `undefined`

**Q3.** Which does NOT change the original array?
- A) `splice`
- B) `sort`
- C) `slice`
- D) `reverse`

**Q4.** What does `[10, 9, 1].sort()` return?
- A) `[1, 9, 10]`
- B) `[10, 9, 1]`
- C) `[1, 10, 9]`
- D) `[9, 10, 1]`

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **C**.
- Q4: **C**. The default sort compares as strings.
