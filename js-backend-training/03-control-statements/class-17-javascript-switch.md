# Class 17: JavaScript Switch

## 1. Definition
The **switch** statement compares one expression against many `case` values and executes the matching block. It is a cleaner alternative to a long `if...else if` chain when comparing one value to fixed options.

## 2. Usage
- Routing by HTTP method (`GET`, `POST`, `PUT`, `DELETE`).
- Handling order status, user roles or event types.
- Command processing in CLI tools and message handlers.

## 3. Description
Syntax:
```js
switch (expression) {
  case value1:
    // code
    break;
  case value2:
    // code
    break;
  default:
    // runs if no case matches
}
```
- Uses **strict equality (`===`)** to compare.
- `break` stops execution. Without it, execution **falls through** to the next case.
- `default` is optional and runs when nothing matches (can be placed anywhere, usually last).
- Several cases can share one block by stacking them.
- For complex conditions (ranges), use `switch (true)` or `if...else`.

## 4. Examples

### Example 1: Day of the week
```js
const day = 3;
let name;
switch (day) {
  case 1: name = "Monday"; break;
  case 2: name = "Tuesday"; break;
  case 3: name = "Wednesday"; break;
  default: name = "Other";
}
console.log(name);   // Wednesday
```

### Example 2: Grouping cases and fall-through
```js
const month = "Feb";
switch (month) {
  case "Jan":
  case "Mar":
  case "May":
    console.log("31 days");
    break;
  case "Feb":
    console.log("28 or 29 days");
    break;
  default:
    console.log("30 days");
}
```

### Example 3: HTTP method router
```js
function handle(method) {
  switch (method.toUpperCase()) {
    case "GET":    return "Fetch data";
    case "POST":   return "Create data";
    case "PUT":    return "Update data";
    case "DELETE": return "Remove data";
    default:       return "405 Method Not Allowed";
  }
}
console.log(handle("post"));    // Create data
console.log(handle("patch"));   // 405 Method Not Allowed
```

## 5. Assignments
1. Build a simple calculator function using `switch` for `+`, `-`, `*`, `/` and an invalid operator message.
2. Print the number of days in a given month using grouped cases (ignore leap years).
3. Write a `getDiscount(role)` function: `"admin"` 30, `"premium"` 20, `"member"` 10, anything else 0.
4. Show what happens when you forget `break` in a switch. Demonstrate the fall-through with output and then fix it.

## 6. MCQs
**Q1.** `switch` compares values using:
- A) `==`
- B) `===`
- C) `!=`
- D) `instanceof`

**Q2.** What happens if `break` is missing from a matching case?
- A) Syntax error
- B) Execution continues into the next case
- C) The switch stops
- D) The default runs only

**Q3.** The `default` block runs:
- A) Always
- B) When no case matches
- C) Before the first case
- D) Only after `break`

**Q4.** With `switch (5) { case "5": ... }`, will the case match?
- A) Yes
- B) No
- C) Only in sloppy mode
- D) Throws an error

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **B**.
- Q4: **B**. `5 === "5"` is false.
