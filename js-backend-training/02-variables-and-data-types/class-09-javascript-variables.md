# Class 09: JavaScript Variables

## 1. Definition
A **variable** is a named container in memory that stores a value. You declare it with `var`, `let` or `const`, then use its name to read or change the value.

## 2. Usage
- Store user input, API responses, configuration and results of calculations.
- Hold database connection settings, tokens and counters in backend code.
- Give meaningful names to values so code is readable.

## 3. Description
- **Declaration**: creates the variable. `let age;`
- **Initialisation**: gives the first value. `age = 25;`
- Both together: `let age = 25;`
- A declared but uninitialised variable holds `undefined`.
- Variable names: letters, digits, `_`, `$`; cannot start with a digit; case sensitive; no reserved words.
- Use `camelCase` (`orderTotal`), constants in `UPPER_SNAKE_CASE` (`MAX_USERS`).
- Multiple variables can be declared in one statement: `let a = 1, b = 2;`
- **Scope** decides where a variable is visible: global, function or block (detailed in the var/let/const classes).

## 4. Examples

### Example 1: Declare, initialise and update
```js
let userName;
console.log(userName);   // undefined
userName = "Sharath";
console.log(userName);   // Sharath
userName = "Kumar";
console.log(userName);   // Kumar
```

### Example 2: Using variables in calculations
```js
const price = 499;
const qty = 3;
const subtotal = price * qty;
console.log(`Subtotal: ${subtotal}`);   // Subtotal: 1497
```

### Example 3: Multiple declarations and swapping
```js
let x = 10, y = 20;
[x, y] = [y, x];
console.log(x, y);   // 20 10
```

## 5. Assignments
1. Declare variables for an employee (id, name, salary, isActive) and print one sentence using all four.
2. Swap two variables with a temporary third variable, then again using destructuring. Compare both.
3. Write a program that stores a temperature in Celsius and prints it in Fahrenheit (`F = C * 9/5 + 32`).
4. Identify the problems in these names and fix them: `1stUser`, `user-name`, `let`, `Total Amount`, `_ok`, `$price`.

## 6. MCQs
**Q1.** What does an uninitialised `let x;` hold?
- A) 0
- B) `null`
- C) `undefined`
- D) Empty string

**Q2.** Which is a valid variable name?
- A) `my-var`
- B) `2name`
- C) `_count`
- D) `new`

**Q3.** Which keyword declares a variable?
- A) `int`
- B) `dim`
- C) `let`
- D) `variable`

**Q4.** Are `Total` and `total` the same variable?
- A) Yes
- B) No
- C) Only in strict mode
- D) Only inside functions

### Answer Key
- Q1: **C**.
- Q2: **C**. Hyphens, leading digits and reserved words are not allowed.
- Q3: **C**. (`var` and `const` also work.)
- Q4: **B**. JavaScript is case sensitive.
