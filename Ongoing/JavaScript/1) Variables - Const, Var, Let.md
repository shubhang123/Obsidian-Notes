
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

