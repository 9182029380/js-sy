# Class 37: JavaScript String Methods

## 1. Definition
**String methods** are built-in functions that search, extract, transform and test text. Because strings are immutable, every method **returns a new value** and leaves the original unchanged.

## 2. Usage
- Cleaning user input (`trim`, `toLowerCase`).
- Validating emails, phone numbers and IDs (`includes`, `startsWith`, `match`).
- Parsing CSV and URLs (`split`, `slice`).
- Formatting output (`padStart`, `toUpperCase`, `replaceAll`).

## 3. Description

| Group | Methods |
|---|---|
| Length / access | `length`, `charAt(i)`, `at(i)`, `charCodeAt(i)` |
| Search | `indexOf`, `lastIndexOf`, `includes`, `startsWith`, `endsWith`, `search`, `match`, `matchAll` |
| Extract | `slice(start, end)`, `substring(start, end)`, `substr` (deprecated) |
| Transform | `toUpperCase`, `toLowerCase`, `trim`, `trimStart`, `trimEnd`, `repeat`, `padStart`, `padEnd` |
| Replace | `replace(a, b)` (first match), `replaceAll(a, b)` |
| Split / join | `split(sep)` returns an array, `join` is an array method |
| Compare | `localeCompare`, `normalize` |

Notes:
- `slice` supports negative indexes, `substring` does not.
- `replace` with a **string** only changes the first match. Use `replaceAll` or a regex with the `g` flag.
- `split("")` splits into characters, `split(" ")` into words.
- Methods chain: `text.trim().toLowerCase().split(" ")`.

## 4. Examples

### Example 1: Search and extract
```js
const email = "  Sharath@Example.com ";
const clean = email.trim().toLowerCase();
console.log(clean);                          // sharath@example.com
console.log(clean.includes("@"), clean.startsWith("sharath"), clean.endsWith(".com"));
console.log(clean.indexOf("@"));             // 7
console.log(clean.slice(0, clean.indexOf("@")));   // sharath
console.log(clean.slice(-3));                // com
```

### Example 2: Replace, split and join
```js
const text = "red,green,blue";
const colors = text.split(",");
console.log(colors);                         // [ 'red', 'green', 'blue' ]
console.log(colors.join(" | "));             // red | green | blue

console.log("a-b-c".replace("-", "_"));      // a_b-c
console.log("a-b-c".replaceAll("-", "_"));   // a_b_c
```

### Example 3: Formatting and regex
```js
console.log("7".padStart(3, "0"));           // 007
console.log("ID".padEnd(5, "."));            // ID...
console.log("ab".repeat(3));                 // ababab
console.log("hello world".replace(/\b\w/g, (c) => c.toUpperCase()));   // Hello World

console.log("Order #123 and #456".match(/\d+/g));   // [ '123', '456' ]
console.log(/^\S+@\S+\.\S+$/.test("a@b.com"));      // true
```

## 5. Assignments
1. Convert `"  the quick brown fox  "` into Title Case (`The Quick Brown Fox`) using trim, split, map and join.
2. Count the number of words in a sentence and print the longest word.
3. Mask a card number: show only the last 4 digits (`**** **** **** 1234`) using `slice` and `padStart`.
4. Write `isValidEmail(email)` using a simple regex and `trim`, then test it with five valid and five invalid inputs.

## 6. MCQs
**Q1.** Which returns a new string without surrounding spaces?
- A) `strip()`
- B) `trim()`
- C) `clean()`
- D) `cut()`

**Q2.** What does `"a-b-c".replace("-", "_")` return?
- A) `"a_b_c"`
- B) `"a_b-c"`
- C) `"a-b-c"`
- D) `"_a-b-c"`

**Q3.** `"hello".slice(-2)` returns:
- A) `"he"`
- B) `"lo"`
- C) `"ll"`
- D) `"o"`

**Q4.** `"a,b,c".split(",")` returns:
- A) `"abc"`
- B) `["a","b","c"]`
- C) `["a,b,c"]`
- D) `3`

### Answer Key
- Q1: **B**.
- Q2: **B**. Only the first match is replaced.
- Q3: **B**.
- Q4: **B**.
