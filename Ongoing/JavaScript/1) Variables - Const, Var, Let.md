
## `const` in JavaScript — Quick Notes
When we use `const`, we **cannot reassign the variable to a new memory address**.  
For **primitive types** (like numbers, strings, booleans), this means the value cannot be changed.  
For **objects, arrays, or maps**, the variable still points to the same address, so we **can modify the contents** inside the object, but we **cannot assign the variable to a new object**.
## in depth:

1. **Meaning:**  
    `const` creates a variable whose **reference cannot be reassigned**.
    
2. **Primitives (`number`, `string`, `boolean`, etc.):**
    
    - Stored as **value**.
        
    - Cannot change the value.
        
    
    ```js
    const x = 10;
    x = 20; // ❌ Error
    ```
    
3. **Objects, Arrays, Maps (reference types):**
    
    - Stored as **memory reference**.
        
    - Reference cannot change, but **contents can be modified**.
        
    
    ```js
    const obj = { name: "Alice" };
    obj.name = "Bob";   // ✅ Allowed
    obj = { name: "Charlie" }; // ❌ Error
    ```
    
4. **Key point:**
    
    - `const` = constant reference, not constant value.
        
    - Primitives → immutable
        
    - Objects → mutable contents
        
5. **Optional:**  
    To make objects fully immutable, use `Object.freeze()`.

Here’s a **quick but detailed version** of notes for `var` and `let`:

---

## **`var`**

- **Reassignable & Redeclarable:** You can change its value and declare it again in the same scope.
    
- **Scope:** Function-scoped (or global if outside a function).
    
- **Hoisting:** Yes, but initialized as `undefined`.
    

```js
var a = 10;
a = 20;       // ✅ Allowed
var a = 30;   // ✅ Allowed
console.log(b); // undefined (hoisted)
```

- **Use case:** Older JavaScript; avoid in modern code due to redeclaration and scope issues.
    

---

## **`let`**

- **Reassignable but NOT Redeclarable:** You can change its value, but cannot declare again in the same block.
    
- **Scope:** Block-scoped `{ }`.
    
- **Hoisting:** Yes, but **not initialized**; accessing before declaration causes an error (Temporal Dead Zone).
    

```js
let x = 10;
x = 20;       // ✅ Allowed
let x = 30;   // ❌ Error
console.log(y); // ❌ Error (TDZ)
```

- **Use case:** Modern JS for variables that can change, safer than `var`.
    

---

✅ **Quick Comparison:**

|Feature|var|let|
|---|---|---|
|Reassignable|✅ Yes|✅ Yes|
|Redeclarable|✅ Yes|❌ No|
|Scope|Function|Block|
|Hoisting|✅ Yes, init undefined|✅ Yes, not initialized|

---

If you want, I can **combine `var`, `let`, `const` in one super-short, exam-ready table** that covers all rules in a glance. Do you want me to do that?