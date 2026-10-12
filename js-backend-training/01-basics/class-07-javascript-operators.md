# Class 07: JavaScript Operators

## 1. Definition
An **operator** is a symbol that performs an operation on one or more values (**operands**) and produces a result. Example: in `a + b`, `+` is the operator and `a`, `b` are operands.

## 2. Usage
Operators are used everywhere: calculating totals, validating input, checking permissions, setting defaults, and building conditions in API handlers.

## 3. Description

| Category | Operators | Notes |
|---|---|---|
| Arithmetic | `+ - * / % **` `++ --` | `%` remainder, `**` power |
| Assignment | `= += -= *= /= %= **=` | `??=`, `\|\|=`, `&&=` also exist |
| Comparison | `== != === !== > < >= <=` | Prefer `===` and `!==` |
| Logical | `&& \|\| !` | Short-circuit evaluation |
| Nullish | `??` | Default only for `null` or `undefined` |
| Ternary | `cond ? a : b` | Inline if-else |
| Optional chaining | `?.` | Safe property access |
| Type | `typeof`, `instanceof` | Check types |
| Bitwise | `& \| ^ ~ << >>` | Rarely used in everyday backend code |
| Spread / rest | `...` | Expand or collect values |

**Strict vs loose equality**: `==` converts types before comparing, `===` does not. Use `===` by default.

**Operator precedence**: `*` and `/` run before `+` and `-`. Use parentheses to make intent clear.

## 4. Examples

### Example 1: Arithmetic and assignment
```js
let a = 10, b = 3;
console.log(a + b, a - b, a * b);   // 13 7 30
console.log(a / b);                 // 3.3333333333333335
console.log(a % b, a ** b);         // 1 1000

let total = 100;
total += 20;    // 120
total *= 2;     // 240
console.log(total);
```

### Example 2: Comparison and logical operators
```js
console.log(5 == "5");    // true  (type coerced)
console.log(5 === "5");   // false (different types)

const age = 25, hasId = true;
console.log(age >= 18 && hasId);   // true
console.log(age < 18 || !hasId);   // false
```

### Example 3: Ternary, nullish and optional chaining
```js
const stock = 0;
console.log(stock > 0 ? "In stock" : "Out of stock");   // Out of stock

const limit = 0;
console.log(limit || 10);   // 10 (0 is falsy)
console.log(limit ?? 10);   // 0  (only null/undefined trigger default)

const req = { user: null };
console.log(req.user?.name ?? "Anonymous");   // Anonymous
```

## 5. Assignments
1. Write a program that takes `price` and `quantity`, calculates subtotal, applies 18% tax using arithmetic operators, and prints the final amount.
2. Check whether a number is even or odd using `%`, and print the result using the ternary operator.
3. Write five comparison expressions that differ in result between `==` and `===`. Explain each.
4. Create `config = { port: 0 }`. Show how `config.port || 3000` and `config.port ?? 3000` produce different values. Explain which is correct for a port number.

## 6. MCQs
**Q1.** What is `10 % 3`?
- A) 3
- B) 1
- C) 0
- D) 3.33

**Q2.** Which is `false`?
- A) `5 == "5"`
- B) `5 === "5"`
- C) `null == undefined`
- D) `1 < 2`

**Q3.** What does `0 ?? 10` return?
- A) 10
- B) 0
- C) `undefined`
- D) `null`

**Q4.** What is the result of `2 + 3 * 4`?
- A) 20
- B) 14
- C) 24
- D) 10

### Answer Key
- Q1: **B**. Remainder of 10 divided by 3.
- Q2: **B**. Strict equality checks type too.
- Q3: **B**. `??` only replaces `null` or `undefined`.
- Q4: **B**. Multiplication has higher precedence.
