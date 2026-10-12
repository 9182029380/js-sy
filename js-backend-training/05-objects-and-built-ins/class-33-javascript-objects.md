# Class 33: JavaScript Objects

## 1. Definition
An **object** is a collection of **key-value pairs** (properties) that models a real-world thing. Values can be any type, including functions (called **methods**).

## 2. Usage
- Representing records: user, order, product, employee.
- JSON request and response bodies in REST APIs.
- Configuration, options and environment settings.
- Grouping related data and behaviour together.

## 3. Description
Creating objects:
- **Literal** (most common): `const user = { name: "Anil", age: 30 };`
- **Constructor / class**: `new User("Anil")`
- **`Object.create(proto)`** to set the prototype.

Working with properties:
- Read: `obj.name` or `obj["name"]` (bracket notation for dynamic or special keys).
- Add or update: `obj.city = "Hyderabad"`.
- Delete: `delete obj.city`.
- Check: `"name" in obj`, `Object.hasOwn(obj, "name")`.
- Shorthand: `{ name, age }`. Computed keys: `{ [key]: value }`.
- Methods: `{ greet() { return "Hi"; } }`; inside, `this` refers to the object.

Useful tools: `Object.keys()`, `Object.values()`, `Object.entries()`, `Object.assign()`, spread `{...a, ...b}`, destructuring `const { name } = user`, `Object.freeze()`, `structuredClone()` for deep copies, `JSON.stringify()` / `JSON.parse()`.

Objects are **reference types**: copying a variable copies the reference, not the object.

## 4. Examples

### Example 1: Create, read, update, delete
```js
const employee = { id: 1, name: "Kiran", dept: "Cloud" };
console.log(employee.name, employee["dept"]);
employee.salary = 90000;       // add
employee.dept = "DevOps";      // update
delete employee.id;            // remove
console.log(employee);
```

### Example 2: Methods, this, destructuring and optional chaining
```js
const account = {
  owner: "Meena",
  balance: 5000,
  deposit(amount) {
    this.balance += amount;
    return this.balance;
  }
};
console.log(account.deposit(1500));   // 6500

const { owner, balance } = account;
console.log(owner, balance);
console.log(account.address?.city);   // undefined, no error
```

### Example 3: Object utilities, copying and JSON
```js
const product = { name: "Pen", price: 10 };
console.log(Object.keys(product), Object.values(product));
console.log(Object.entries(product));

const copy = { ...product, price: 12 };       // shallow copy with change
const deep = structuredClone({ a: { b: 1 } }); // deep copy
console.log(copy, deep);

const text = JSON.stringify(product);          // object to JSON string
console.log(text, JSON.parse(text).name);
```

## 5. Assignments
1. Create a `student` object with name, age, marks (array) and a method `average()` that returns the average marks.
2. Given `{ a: 1, b: 2, c: 3 }`, create a new object with every value doubled using `Object.entries()` and `Object.fromEntries()`.
3. Merge two config objects (defaults and overrides) with spread so overrides win. Print the result.
4. Demonstrate that `const a = {x:1}; const b = a; b.x = 2;` changes `a`, then fix it with a copy. Explain the difference between shallow and deep copy.

## 6. MCQs
**Q1.** Which creates an object?
- A) `const o = [1,2];`
- B) `const o = { a: 1 };`
- C) `const o = (a: 1);`
- D) `const o = <a:1>;`

**Q2.** How do you read a property with a variable key?
- A) `obj.key`
- B) `obj[key]`
- C) `obj->key`
- D) `obj::key`

**Q3.** `const b = a;` where `a` is an object means:
- A) `b` is a new independent copy
- B) `b` points to the same object
- C) `b` is a string
- D) Error

**Q4.** Which makes a deep copy?
- A) `{ ...obj }`
- B) `Object.assign({}, obj)`
- C) `structuredClone(obj)`
- D) `const b = obj`

### Answer Key
- Q1: **B**.
- Q2: **B**.
- Q3: **B**.
- Q4: **C**. Spread and `Object.assign` are shallow.
