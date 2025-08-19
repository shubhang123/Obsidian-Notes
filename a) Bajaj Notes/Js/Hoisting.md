# In-Depth Knowledge: Hoisting in JavaScript

## 1. What is Hoisting?

**Hoisting** is an internal behavior of JavaScript where declarations (variables, functions, classes) are processed before any code executes. During the *creation phase* of every execution context, the JS engine scans code for declarations and "hoists" them—allocating memory and setting up references—prior to actually running statements. This explains why you can sometimes reference variables or invoke functions before they appear later in code.

## 2. Execution Context & Phases

JavaScript executes in two main phases:
- **Creation (or Memory Allocation) Phase**
    - Scope is determined
    - Variables/functions/classes are hoisted, memory is reserved
    - Variables (`var`) are initialized as `undefined` at this stage
    - `let`/`const` and classes are hoisted but NOT initialized (see Temporal Dead Zone)
- **Execution Phase**
    - Code is run line-by-line
    - Assignments and invocations happen

## 3. Variable Hoisting: var, let, const

### `var`
- **Hoisted, initialized as `undefined`**
- Can be referenced before declaration but will return `undefined`
- Has *function scope*
- Allows redeclaration

```javascript
console.log(a); // undefined
var a = 5;
console.log(a); // 5
```

### `let` and `const`
- **Hoisted, NOT initialized**
- Enter a *Temporal Dead Zone* (TDZ)—cannot be accessed before their declaration, or you'll get a `ReferenceError`
- Have *block scope* (confined to `{}` blocks)
- `const` must be assigned immediately after declaration

```javascript
console.log(b); // ReferenceError
let b = 10;

console.log(c); // ReferenceError
const c = 20;
```

**Temporal Dead Zone (TDZ):**  
From the start of the scope to the line where a variable is declared. During TDZ, any access throws an error.

## 4. Function Hoisting

### Function Declarations
- **Fully hoisted:** both the name and the function body
- Can be called anywhere in their scope—even before the declaration appears
```javascript
foo(); // works!
function foo() { console.log('Hello'); }
```

### Function Expressions & Arrow Functions
- Only the *variable* is hoisted (using `var`, `let`, or `const`)
- The assigned function is NOT hoisted
- Using them before declaration leads to `TypeError` (with `var`) or `ReferenceError` (with `let`/`const`)

```javascript
bar(); // TypeError: bar is not a function
var bar = function() { ... };

baz(); // ReferenceError
let baz = () => { ... };
```

## 5. Class Hoisting

- Classes (declared with `class`) are hoisted but NOT initialized
- They also fall within TDZ — using before declaration throws `ReferenceError`
```javascript
const inst = new Test(); // ReferenceError
class Test {}
```

## 6. Hoisting in Modules (`import`, `export`)

- ES6 module imports and exports are *hoisted* to the top of the file
- All imports are resolved before any code runs, and their variables are available everywhere (with TDZ applied)

## 7. Scope & Shadowing

- Hoisting is **scope-based**
    - `var` is function-scoped
    - `let`/`const` are block-scoped
    - Functions and classes are scoped according to their declaration context
- **Shadowing:** Variable or function in an inner scope with the same name as an outer scope "shadows" (hides) the outer one

## 8. Pitfalls & Best Practices

**Common mistakes:**
- Using variables before declarations (`var` returns `undefined`—often mistaken for bugs)
- Accessing `let`/`const` or classes before declaration (throws `ReferenceError`)
- Confusing function declarations and expressions
- Redeclaring variables with `var`, especially in nested scopes

**Best Practices:**
- Always declare variables and functions at the top of their scope
- Prefer `let` and `const` for block scoping and TDZ protection
- Use function declarations when you need hoisting, expressions when you don’t
- Minimize variable shadowing for clarity
- Avoid relying on hoisting; write code as if declarations are NOT moved
- Enable `"use strict"` mode for error checks

## 9. Deep-Dive: Temporal Dead Zone (TDZ)

- Any variable declared with `let`, `const`, or `class` is in the TDZ from the start of its scope until its declaration is processed
- Accessing during TDZ yields an error, preventing use of uninitialized variables

## 10. Advanced: Inner Functions, Closures & Hoisting

- **Inner function declarations are hoisted within their containing function**
- Functions declared inside blocks (`if`, `for`) may have unpredictable hoisting behavior—stick to declarations at top-level or inside functions for clarity

## 11. Hoisting & Strict Mode

Strict mode (`"use strict"`) doesn’t change hoisting itself, but:
- Catches accidental globals
- Prohibits some silent errors
- Makes TDZ and scoping rules stricter

## 12. Visualization Table

| Feature           | Scope         | Hoisted? | Initialized?    | Access Before Declaration       |
|-------------------|--------------|----------|-----------------|-------------------------------|
| var               | Function     | Yes      | Yes:`undefined` | Returns `undefined`           |
| let               | Block        | Yes      | No              | `ReferenceError` (TDZ)        |
| const             | Block        | Yes      | No              | `ReferenceError` (TDZ)        |
| function decl.    | Function/Block| Yes     | Yes (body)      | Works normally                |
| function expr.    | As variable  | Yes (var)| No              | `undefined` or `ReferenceError`|
| arrow function    | As variable  | Yes (var)| No              | `undefined` or `ReferenceError`|
| class             | Block        | Yes      | No              | `ReferenceError` (TDZ)        |

***

## 13. Real-World Example

```javascript
console.log(foo);      // undefined
var foo = 2;

console.log(bar);      // ReferenceError
let bar = 3;

console.log(baz);      // ReferenceError
const baz = 4;

console.log(bop());    // "hi"
function bop() { return "hi"; }

console.log(qux);      // undefined
var qux = function() { return "hello"; };
console.log(qux());    // "hello"

console.log(quux);     // ReferenceError
let quux = () => "yo";
```

***

**Mastering hoisting** is crucial for understanding JavaScript's execution and scope behaviors and for writing robust, bug-resistant code. Always treat hoisting as an invisible force: expect only declarations (not initializations!) to move, and never rely on variables, functions, or classes being accessible before their explicit declaration.

If you want deep explorations or real-world scenarios on individual topics (TDZ, class hoisting, arrow function nuances, shadowing synergies), specify and each will be broken down with further examples and advanced explanations.