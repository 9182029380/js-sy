# Class 36: JavaScript Strings

## 1. Definition
A **string** is a sequence of characters used to represent text. Strings are **primitive** and **immutable** (they cannot be changed in place, operations return new strings).

## 2. Usage
- Names, emails, messages, URLs, file paths.
- Building SQL/HTTP text, logs and responses.
- Parsing and formatting data (CSV lines, JSON text, query strings).
- Validation (length, patterns).

## 3. Description
Creating strings:
```js
const a = 'single';
const b = "double";
const c = `template with ${1 + 1}`;   // backticks: interpolation and multi-line
```
- **Template literals** support `${expression}` and multi-line text.
- **Escape sequences**: `\n` new line, `\t` tab, `\"` quote, `\\` backslash.
- **Index access**: `str[0]`, `str.at(-1)`. `str.length` gives the length.
- **Immutable**: `str[0] = "X"` does nothing.
- Compare with `===`. Case-sensitive.
- **Concatenate** with `+` or template literals.
- Unicode: emoji and some characters count as 2 in `length` (UTF-16). Use `[...str]` to count characters.
- Strings are **iterable** (`for...of` goes over characters).
- Convert: `String(123)`, `Number("42")`, `parseInt("42px")`, `parseFloat("3.14abc")`.

## 4. Examples

### Example 1: Creating and accessing
```js
const name = "Sharath";
console.log(name.length, name[0], name.at(-1));   // 7 S h
console.log(`Hello, ${name}! 2 + 3 = ${2 + 3}`);

const multi = `Line 1
Line 2`;
console.log(multi);
```

### Example 2: Immutability and concatenation
```js
let s = "hello";
s[0] = "J";
console.log(s);                // hello (unchanged)
s = "J" + s.slice(1);
console.log(s);                // Jello
console.log("5" + 3, "5" * 3); // 53 15
```

### Example 3: Escapes, comparison and Unicode
```js
console.log("He said \"hi\"\nNew line\tTab");
console.log("a" === "A", "apple" < "banana");   // false true
console.log("😀".length, [..."😀"].length);       // 2 1
for (const ch of "JS") console.log(ch);
```

## 5. Assignments
1. Read a full name string and print it in the format `Last, First` using string operations.
2. Check whether a string is a palindrome (ignore case and spaces).
3. Count how many times each character appears in a string and print the counts using an object.
4. Build a multi-line invoice text using a template literal with customer name, three item lines and the total.

## 6. MCQs
**Q1.** Which creates an interpolated string?
- A) `"Hi ${name}"`
- B) `'Hi ${name}'`
- C) `` `Hi ${name}` ``
- D) `(Hi ${name})`

**Q2.** Strings in JavaScript are:
- A) Mutable
- B) Immutable
- C) Objects only
- D) Arrays

**Q3.** What does `"5" + 3` give?
- A) 8
- B) `"53"`
- C) `NaN`
- D) Error

**Q4.** What does `"abc".at(-1)` return?
- A) `"a"`
- B) `"b"`
- C) `"c"`
- D) `undefined`

### Answer Key
- Q1: **C**. Only backticks interpolate.
- Q2: **B**.
- Q3: **B**.
- Q4: **C**.
