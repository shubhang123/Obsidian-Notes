

## `const` in JavaScript — Quick Notes

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
    

---

If you want, I can make an **even snappier one-line version** for easy memorization. Do you want me to do that?