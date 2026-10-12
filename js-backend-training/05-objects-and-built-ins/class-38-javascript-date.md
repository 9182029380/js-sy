# Class 38: JavaScript Date

## 1. Definition
The **Date** object represents a single moment in time, stored internally as the number of **milliseconds since 1 January 1970 00:00:00 UTC** (the Unix epoch).

## 2. Usage
- Timestamps on records (`createdAt`, `updatedAt`).
- Expiry of tokens, sessions and cache entries.
- Scheduling, reports, date filters and age calculations.
- Measuring durations (`Date.now()` before and after).

## 3. Description
Creating dates:
```js
new Date()                          // now
new Date("2026-10-11T10:30:00Z")    // ISO string (UTC with Z)
new Date(2026, 9, 11, 10, 30)       // year, monthIndex (0-11!), day, hour, min
new Date(1760178600000)             // from milliseconds
Date.now()                          // current time in ms (number)
```
Getters: `getFullYear()`, `getMonth()` (**0 to 11**), `getDate()` (day of month), `getDay()` (0 = Sunday), `getHours()`, `getMinutes()`, `getTime()`. UTC versions: `getUTCHours()` etc.
Setters: `setDate()`, `setMonth()`, `setFullYear()`, `setHours()`.
Output: `toISOString()` (UTC, best for APIs and databases), `toLocaleDateString("en-IN")`, `toLocaleString("en-IN", { timeZone: "Asia/Kolkata" })`, `toJSON()`.

Rules to remember:
- **Months start at 0.**
- Subtracting two dates gives **milliseconds**.
- Invalid dates produce `Invalid Date` and `NaN` from `getTime()`.
- Dates are **mutable**. Copy before changing: `new Date(d)`.
- Store and transfer times in **UTC / ISO format**, convert to local time only for display.

## 4. Examples

### Example 1: Create and read parts
```js
const d = new Date("2026-10-11T10:30:00Z");
console.log(d.toISOString());            // 2026-10-11T10:30:00.000Z
console.log(d.getUTCFullYear(), d.getUTCMonth() + 1, d.getUTCDate());   // 2026 10 11
console.log(d.getTime());                // ms since epoch
console.log(d.toLocaleDateString("en-IN", { timeZone: "Asia/Kolkata" }));
```

### Example 2: Date arithmetic
```js
const start = new Date("2026-01-01");
const end = new Date("2026-03-01");
const days = (end - start) / (1000 * 60 * 60 * 24);
console.log(days);   // 59

const due = new Date("2026-10-11T00:00:00Z");
due.setUTCDate(due.getUTCDate() + 30);
console.log(due.toISOString());   // 2026-11-10T00:00:00.000Z
```

### Example 3: Timing code and validating dates
```js
const t0 = Date.now();
let s = 0;
for (let i = 0; i < 1e6; i++) s += i;
console.log("Took", Date.now() - t0, "ms");

const bad = new Date("not a date");
console.log(isNaN(bad.getTime()));   // true
```

## 5. Assignments
1. Write `daysBetween(dateA, dateB)` returning the number of days between two date strings.
2. Calculate a person's age in years from a birth date string.
3. Print the current date in the format `DD-MM-YYYY` using getters and `padStart`.
4. Write `addDays(date, n)` that returns a new Date without modifying the original. Show that the original did not change.

## 6. MCQs
**Q1.** What does `new Date(2026, 0, 15)` represent?
- A) 15 January 2026
- B) 15 February 2026
- C) 15 December 2025
- D) Invalid date

**Q2.** `new Date("2026-03-01") - new Date("2026-01-01")` returns:
- A) Days
- B) Milliseconds
- C) A Date
- D) Seconds

**Q3.** Which method gives an ISO UTC string?
- A) `toString()`
- B) `toISOString()`
- C) `toLocaleString()`
- D) `toDateString()`

**Q4.** What does `getDay()` return?
- A) Day of the month
- B) Day of the week (0 to 6)
- C) Day of the year
- D) Number of days in the month

### Answer Key
- Q1: **A**. Month index 0 is January.
- Q2: **B**.
- Q3: **B**.
- Q4: **B**. `getDate()` is the day of the month.
