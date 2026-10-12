# Class 16: JavaScript if-else

## 1. Definition
The **if-else** statement runs a block of code only when a condition is true, and optionally runs a different block when it is false. Variants: `if`, `if...else`, `if...else if...else`, and the ternary operator.

## 2. Usage
- Validating request data (is the email present? is the age valid?).
- Authorisation checks (is the user an admin?).
- Choosing logic by status code, user role, payment state or feature flag.

## 3. Description
Syntax:
```js
if (condition) {
  // runs when condition is truthy
} else if (otherCondition) {
  // runs when otherCondition is truthy
} else {
  // runs otherwise
}
```
- The condition is converted to a boolean (truthy/falsy).
- Conditions are checked top to bottom, **the first match wins**.
- Always use braces `{}` even for one line, to prevent bugs.
- Use **guard clauses** (return early on invalid input) to avoid deep nesting.
- Ternary shortcut: `condition ? valueIfTrue : valueIfFalse`.

## 4. Examples

### Example 1: if...else
```js
const age = 20;
if (age >= 18) {
  console.log("Eligible to vote");
} else {
  console.log("Not eligible");
}
```

### Example 2: if...else if...else (grade calculator)
```js
const marks = 72;
let grade;
if (marks >= 90) {
  grade = "A+";
} else if (marks >= 75) {
  grade = "A";
} else if (marks >= 60) {
  grade = "B";
} else if (marks >= 40) {
  grade = "C";
} else {
  grade = "Fail";
}
console.log(grade);   // B
```

### Example 3: Guard clauses in a backend-style function
```js
function createUser(input) {
  if (!input) return { status: 400, error: "Body required" };
  if (!input.email) return { status: 400, error: "Email required" };
  if (input.age < 18) return { status: 403, error: "Must be 18+" };
  return { status: 201, message: "User created" };
}
console.log(createUser({ email: "a@b.com", age: 25 }));
console.log(createUser({ age: 25 }));
```

## 5. Assignments
1. Write a program to find the largest of three numbers using `if...else if...else`.
2. Check if a given year is a leap year (divisible by 4, but not by 100 unless also divisible by 400).
3. Write a function `shippingCharge(weightKg)` returning 0 for weight up to 1, 50 for up to 5, 120 for up to 10, and 200 above that.
4. Write a `login(user, password)` function with guard clauses that returns different status messages for missing user, wrong password and success.

## 6. MCQs
**Q1.** Which values make an `if` condition false?
- A) `"0"`
- B) `[]`
- C) `0`
- D) `"false"`

**Q2.** In an if/else-if chain, if two conditions are true, which block runs?
- A) Both
- B) The last one
- C) The first true one only
- D) None

**Q3.** What does `console.log(5 > 3 ? "yes" : "no")` print?
- A) `no`
- B) `yes`
- C) `true`
- D) `undefined`

**Q4.** A guard clause is used to:
- A) Loop faster
- B) Exit early on invalid conditions
- C) Declare variables
- D) Create classes

### Answer Key
- Q1: **C**. Strings and empty arrays are truthy.
- Q2: **C**.
- Q3: **B**.
- Q4: **B**.
