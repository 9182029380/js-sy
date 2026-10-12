# Class 30: JavaScript Function - call()

## 1. Definition
`call()` is a method available on every function. It **invokes the function immediately** with a chosen value for `this` and arguments passed **one by one**.

Syntax: `func.call(thisArg, arg1, arg2, ...)`

## 2. Usage
- Borrowing a method from one object to use on another.
- Controlling `this` explicitly when a function is called.
- Calling parent "constructors" in older inheritance patterns.
- Using array or string methods on array-like objects.

## 3. Description
- `this` inside a function depends on **how it is called**. `call()` lets you set it directly.
- The function **runs right away** (unlike `bind()`, which returns a new function).
- Arguments are listed **separately** (unlike `apply()`, which takes an array).
- If `thisArg` is `null` or `undefined` in non-strict mode, `this` becomes the global object. In strict mode it stays `null` or `undefined`.
- **Arrow functions ignore `call()`**'s `this` because they use the `this` of the surrounding scope.

## 4. Examples

### Example 1: Setting `this`
```js
function introduce(greeting, punctuation) {
  return `${greeting}, I am ${this.name}${punctuation}`;
}
const person1 = { name: "Anil" };
const person2 = { name: "Ravi" };

console.log(introduce.call(person1, "Hello", "!"));    // Hello, I am Anil!
console.log(introduce.call(person2, "Hi", "."));       // Hi, I am Ravi.
```

### Example 2: Borrowing a method
```js
const account = {
  owner: "Kiran",
  describe() { return `Account owner: ${this.owner}`; }
};
const other = { owner: "Meena" };
console.log(account.describe.call(other));   // Account owner: Meena
```

### Example 3: Using array methods on array-like objects
```js
const arrayLike = { 0: "a", 1: "b", 2: "c", length: 3 };
const result = Array.prototype.map.call(arrayLike, (x) => x.toUpperCase());
console.log(result);   // [ 'A', 'B', 'C' ]
```

## 5. Assignments
1. Create a function `showSalary()` that prints `this.name` and `this.salary`. Call it with two different employee objects using `call()`.
2. Borrow the `fullName()` method from one person object to use on another that has `first` and `last` properties.
3. Use `Math.max.call(null, 3, 9, 5)` and explain why `null` is fine as `this` here.
4. Show what happens when you use `call()` on an arrow function that uses `this`. Explain why.

## 6. MCQs
**Q1.** What does `call()` do?
- A) Returns a new function
- B) Invokes the function immediately with a given `this`
- C) Delays the function
- D) Deletes the function

**Q2.** How are arguments passed to `call()`?
- A) As an array
- B) Individually, after `thisArg`
- C) As an object
- D) Not allowed

**Q3.** Which method returns a new function instead of calling it?
- A) `call()`
- B) `apply()`
- C) `bind()`
- D) `run()`

**Q4.** `call()` can change the `this` of:
- A) Arrow functions
- B) Regular functions
- C) Both equally
- D) Neither

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **C**.
- Q4: **B**. Arrow functions keep their lexical `this`.
