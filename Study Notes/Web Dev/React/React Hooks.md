# useMemo Hook?

The **useMemo** hook is a built-in React hook that helps optimize performance by **memoizing** (caching) the result of a computation and reusing it unless its dependencies change. This prevents expensive computations from being re-executed unnecessarily during component re-renders.[1][2]

### Syntax

```javascript
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

The hook takes two arguments:[2][3]
- **First argument**: A function that returns the computed value
- **Second argument**: An array of dependencies that controls when the function should be re-evaluated

## Why Store useMemo Inside a Variable?

The reason we store `useMemo` inside a variable is because **it returns a memoized value**. The hook doesn't store the function itself - it stores the **result** of the function.[4][5][6][1]

Here's what happens:[3]
1. **During the first render**: React invokes the function and calculates the value
2. **On subsequent renders**: React checks if any dependencies have changed
   - If dependencies haven't changed: React reuses the previously calculated value
   - If dependencies have changed: React re-runs the function to calculate a new value

**Whatever we return from the function is assigned to the variable**. This cached value can then be used throughout the component without triggering expensive recalculations.[3]

## How is useMemo Used?

### Basic Example

```javascript
import React, { useMemo } from 'react';

const MyComponent = ({ data }) => {
  // Memoize the result of the expensive computation
  const memoizedValue = useMemo(() => {
    // Perform some expensive computation using the data
    return processData(data);
  }, [data]); // Dependency array: recompute if 'data' changes

  return (
    
      {memoizedValue}
    
  );
};
```

### Practical Example: Preventing Unnecessary Re-renders

One common use case is preventing child components from re-rendering unnecessarily:[4]

```javascript
export default function TodoList({ todos, tab, theme }) {
  // Without useMemo, filterTodos always creates a different array
  // causing child components to re-render unnecessarily
  
  const visibleTodos = useMemo(
    () => filterTodos(todos, tab),
    [todos, tab] // Only recalculate when todos or tab changes
  );

  return (
    
      
    
  );
}
```

**Without useMemo**: The `filterTodos` function always creates a different array, meaning the `List` component's props are never the same and it re-renders every time.[4]

**With useMemo**: The calculation is cached, ensuring the `List` component receives the same props between re-renders (when dependencies don't change), allowing it to skip unnecessary re-renders.[4]


## Key Benefits

1. **Performance Optimization**: Prevents expensive calculations from running on every render[7][2]
2. **Referential Equality**: Maintains the same reference for objects/arrays when dependencies don't change[8]
3. **Child Component Optimization**: Helps prevent unnecessary re-renders of child components that depend on memoized values[4]

## When to Use useMemo

- **Expensive computations**: When you have calculations that take significant time to execute[9]
- **Object/array values**: For referential integrity when passing objects or arrays as props[8]
- **Optimizing child components**: When working with components wrapped in `React.memo`[4]

## Important Considerations

- **Don't overuse it**: Using `useMemo` unnecessarily can hurt performance by adding overhead[9]
- **Dependencies matter**: Always include all values from component scope that are used inside the memoized function in the dependency array[2]
- **useMemo vs useCallback**: `useMemo` caches the **return value** of a function, while `useCallback` caches the **function definition** itself[5][6]

The useMemo hook is essentially like a cache with dependencies as the cache invalidation strategy, making it a powerful tool for React performance optimization when used appropriately.[3]

# useCallback Hook?

The **useCallback** hook is a built-in React hook that **memoizes a callback function** and prevents it from being recreated on every render unless its dependencies change. Unlike `useMemo` which caches the return value of a function, `useCallback` caches the **function definition itself**.[1][2][5]

### Syntax

```javascript
const memoizedCallback = useCallback(() => {
  // Your callback logic here
}, [dependency1, dependency2, ...]);
```

The hook takes two arguments:[2][6]
- **First argument**: The function you want to memoize
- **Second argument**: An array of dependencies that determine when the function should be recreated

## How useCallback Works

When you use `useCallback`, React follows this process:[6]

1. **On initial render**: React creates the function and returns it
2. **On subsequent renders**: React checks if any values in the dependency array have changed
   - **If dependencies haven't changed**: Returns the same function instance from the previous render
   - **If dependencies have changed**: Creates a new function instance and returns it

This ensures that **the exact same function instance is returned** every time the component re-renders, as long as the dependencies don't change.[6]

## Why Use useCallback?

### The Problem: Function Recreation

In React, callback functions like event handlers create **new function objects at every re-render** of the component. This breaks referential equality and can cause unnecessary re-renders in child components.[5]

Here's an example **without useCallback**:[2]

```javascript
// Without useCallback
function WithoutCallbackExample() {
  const [count1, setCount1] = useState(0);
  const [count2, setCount2] = useState(0);

  // These functions are recreated on EVERY render
  const handleClick1 = () => {
    setCount1(count1 + 1);
  };

  const handleClick2 = () => {
    setCount2(count2 + 1);
  };

  return (
    
      
      
    
  );
}
```

**Problem**: All child components re-render every time because they receive new function references.[2]

### The Solution: useCallback

```javascript
// With useCallback
function WithCallbackExample() {
  const [count1, setCount1] = useState(0);
  const [count2, setCount2] = useState(0);

  // These functions are memoized and only recreated when dependencies change
  const handleClick1 = useCallback(() => {
    setCount1(count1 + 1);
  }, [count1]);

  const handleClick2 = useCallback(() => {
    setCount2(count2 + 1);
  }, [count2]);

  return (
    
      
      
    
  );
}
```

**Result**: Only the relevant button re-renders when its specific handler changes.[2]

## Practical Example: Preventing Child Re-renders

```javascript
function ParentComponent() {
  const [count, setCount] = useState(0);
  
  const increment = useCallback(() => {
    setCount(c => c + 1);
  }, []); // Empty dependency array means this function never changes

  return (
    
      Count: {count}
      
    
  );
}

const ChildComponent = React.memo(({ onIncrement }) => {
  console.log('ChildComponent rendered');
  return Increment;
});
```

In this example:[6]
- `increment` is memoized and never changes (empty dependency array)
- `ChildComponent` is wrapped with `React.memo` to prevent unnecessary re-renders
- The child component **won't re-render** when `count` changes because the `onIncrement` prop reference stays the same

## useCallback vs useMemo

| Aspect | useCallback | useMemo |
|--------|-------------|---------|
| **Returns** | Memoized **function** | Memoized **value** |
| **Purpose** | Prevents function recreation | Avoids recalculating values |
| **Use Case** | Event handlers, function props | Expensive computations |

### Example Comparison:[5]

**Using useMemo**:
```javascript
const filteredItems = useMemo(() => {
  return items.filter(item => item.active);
}, [items]);

return ;
```

**Using useCallback**:
```javascript
const getFilteredItems = useCallback(() => {
  return items.filter(item => item.active);
}, [items]);

return ;
```

## When to Use useCallback

1. **Preventing child re-renders**: When passing functions as props to components wrapped in `React.memo`[5]
2. **Event handlers**: To maintain function reference consistency[5]
3. **Dependency optimization**: When functions are dependencies in other hooks like `useEffect`

## Common Pitfall

**Without proper dependencies**:[7]
```javascript
const funcSet = new Set();

const App = () => {
  const [cnt, setCnt] = useState(0);
  
  const incCnt = () => setCnt(cnt + 1); // New function every render
  
  funcSet.add(incCnt);
  alert(funcSet.size); // Will keep growing!
  
  return Increase;
};
```

Every render creates a new function, causing the Set size to continuously grow and leading to performance issues.

The `useCallback` hook is essential for optimizing React applications by ensuring function references remain stable, preventing unnecessary re-renders and improving overall performance.

[1] https://react.dev/reference/react/useCallback
[2] https://www.w3schools.com/react/react_usecallback.asp
[3] https://semaphore.io/blog/react-usecallback-hook
[4] https://www.youtube.com/watch?v=_AyFP5s69N4
[5] https://refine.dev/blog/react-usecallback-guide/
[6] https://hygraph.com/blog/react-usecallback-a-complete-guide
[7] https://www.geeksforgeeks.org/reactjs/react-js-usecallback-hook/
[8] https://stackoverflow.com/questions/71265042/what-is-usecallback-in-react-and-when-to-use-it
[9] https://coderpad.io/blog/development/a-guide-to-using-reacts-usecallback-hook/



# UseEffect 
The **useEffect hook** in React lets you perform side effects in functional components, such as fetching data, updating the DOM, or setting up subscriptions.[1][2][4][5][6]

- **Syntax and Usage:**
  ```javascript
  useEffect(() => {
    // side effect logic
    return () => {
      // cleanup logic (optional)
    };
  }, [dependencies]); // dependencies array (optional)
  ```
  - The first argument is a function containing the side effect code.
  - The second argument is an optional array of dependencies; the effect runs whenever a value in this array changes. If empty, it runs only after the initial render.[4][5][1]

- **Behavior:**
  - Without dependencies, useEffect runs after every render.
  - With an empty dependency array (`[]`), it only runs after the initial render.
  - If you include specific variables in the array, it runs whenever those change.[5][1][4]

- **Lifecycle Replacement:**
  - It replaces class component lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.[3][6][5]
  - The optional return function in useEffect acts as a cleanup, similar to `componentWillUnmount`.

- **Common Use Cases:**
  - Data fetching from APIs.
  - Setting up event listeners.
  - Managing timers.
  - Cleaning up resources when the component unmounts.[6][4][5]

- **Example:**
  ```javascript
  import React, { useState, useEffect } from 'react';

  function Example() {
    const [count, setCount] = useState(0);

    useEffect(() => {
      document.title = `You clicked ${count} times`;
    }, [count]);

    return (
      
        You clicked {count} times
         setCount(count + 1)}>Click me
      
    );
  }
  ```
  In this example, the document title updates whenever `count` changes.[3]

- **Cleanup Example:**
  ```javascript
  useEffect(() => {
    const timer = setTimeout(() => {
      // perform action
    }, 1000);
    return () => clearTimeout(timer);
  }, []);
  ```
  This cleans up the timer when the component unmounts or before rerunning the effect.[4][5]

The useEffect hook is a core part of modern React development and allows for centralized management of side effects within function components, improving readability and maintainability.[5]

[1] https://www.w3schools.com/react/react_useeffect.asp
[2] https://react.dev/reference/react/useEffect
[3] https://legacy.reactjs.org/docs/hooks-effect.html
[4] https://www.geeksforgeeks.org/reactjs/reactjs-useeffect-hook/
[5] https://hygraph.com/blog/react-useeffect-a-complete-guide
[6] https://www.freecodecamp.org/news/react-hooks-useeffect-usestate-and-usecontext/
[7] https://www.youtube.com/watch?v=-4XpG5_Lj_o
[8] https://radixweb.com/blog/guide-to-useeffect-hook-in-react
[9] https://react.dev/reference/react/hooks