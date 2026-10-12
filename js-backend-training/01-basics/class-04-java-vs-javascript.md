# Class 04: Difference between Java and JavaScript

## 1. Definition
**Java** is a statically typed, class-based, compiled (to bytecode) language that runs on the JVM. **JavaScript** is a dynamically typed, prototype-based language run by an engine such as V8. They are **different languages** that only share part of a name for historical marketing reasons.

## 2. Usage
Many backend teams use both: Java (Spring Boot) for large enterprise services and Node.js for APIs, gateways and real-time services. Developers moving from Java to JS must understand the differences to avoid common mistakes.

## 3. Description
| Point | Java | JavaScript |
|---|---|---|
| Typing | Static, types declared and checked at compile time | Dynamic, types checked at runtime |
| Execution | Compiled to bytecode, runs on JVM | Interpreted / JIT by an engine (V8) |
| OOP model | Class-based | Prototype-based (`class` is syntax over prototypes) |
| Threads | Multi-threaded | Single-threaded with event loop |
| Concurrency | Threads, executors | Callbacks, Promises, `async/await` |
| Variable declaration | `int x = 5;` | `let x = 5;` |
| Entry point | `public static void main` | Top of file, no main required |
| Build | Maven or Gradle, compile step | No compile step (TypeScript optional) |
| Equality | `==` compares primitives, `.equals()` for objects | `===` strict, `==` loose with coercion |
| Typical backend | Spring Boot | Express, NestJS |
| Files | `.java` / `.class` | `.js` / `.mjs` |

## 4. Examples

### Example 1: Hello World side by side
```java
// Java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```
```js
// JavaScript
console.log("Hello");
```

### Example 2: Typing
```java
// Java: compile error if types do not match
int count = 10;
// count = "ten";  // error
```
```js
// JavaScript: allowed
let count = 10;
count = "ten";
console.log(count);
```

### Example 3: Same logic, class syntax
```java
class Employee {
    String name;
    Employee(String name) { this.name = name; }
    String greet() { return "Hi " + name; }
}
```
```js
class Employee {
  constructor(name) { this.name = name; }
  greet() { return `Hi ${this.name}`; }
}
console.log(new Employee("Ravi").greet());
```

## 5. Assignments
1. Prepare a one-page comparison of Java and JavaScript with at least eight differences in your own words.
2. Translate this Java loop to JavaScript: `for (int i = 1; i <= 5; i++) { System.out.println(i * i); }`
3. Show with code why `"5" == 5` is `true` but `"5" === 5` is `false` in JS. Then explain which Java operator behaves closest to `===`.
4. Explain, with a short example, why a Java developer might see a bug in `let total = "10" + 5;` in JavaScript.

## 6. MCQs
**Q1.** Which is true about Java and JavaScript?
- A) JavaScript is a lighter version of Java
- B) They are different languages
- C) JavaScript is compiled to JVM bytecode
- D) Java is dynamically typed

**Q2.** JavaScript uses which inheritance model?
- A) Prototype-based
- B) Only multiple class inheritance
- C) Interface-only
- D) None

**Q3.** Which entry point is required in JavaScript?
- A) `public static void main`
- B) `function main()`
- C) None, code runs from the top of the file
- D) `start()`

**Q4.** Which describes Java typing?
- A) Static
- B) Dynamic
- C) Untyped
- D) Weak only

### Answer Key
- Q1: **B**.
- Q2: **A**.
- Q3: **C**.
- Q4: **A**. Java types are fixed and checked at compile time.
