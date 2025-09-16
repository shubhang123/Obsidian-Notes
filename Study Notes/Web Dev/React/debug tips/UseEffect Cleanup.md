The issue occurs because of a fundamental difference in **how React's useEffect cleanup function works** versus calling a regular function. In your first code, `useEffect` properly handles the cleanup lifecycle, but in your second attempt, you're not returning the cleanup function correctly from the effect.

## Why the First Approach Works

When you put the logic directly inside `useEffect`, React can properly manage the cleanup lifecycle. The cleanup function you return is automatically called when:[1][2]
- The component unmounts
- The dependencies change and the effect needs to run again

```javascript
useEffect(() => {
    if (isOpen) {
        // Effect runs
        window.history.pushState({ youtubePlayerOpen: true }, '');
        const handlePopState = () => onClose();
        window.addEventListener('popstate', handlePopState);

        // React calls this cleanup when needed
        return () => {
            window.removeEventListener('popstate', handlePopState);
            if (window.history.state?.youtubePlayerOpen) {
                window.history.back();
            }
        };
    }
    return () => {}; // Empty cleanup for when isOpen is false
}, [isOpen, onClose]);
```

## Why the Second Approach Doesn't Work

In your second approach, you're **calling** `handleYTBackButton()` inside `useEffect`, but you're **not returning** its result. The function executes immediately and returns the cleanup function, but React never receives it:[3][1]

```javascript
const handleYTBackButton = () => {
    // This function executes immediately when called
    if (isOpen) {
        window.history.pushState({ youtubePlayerOpen: true }, '');
        const handlePopState = () => onClose();
        window.addEventListener('popstate', handlePopState);

        // This cleanup function is returned but lost
        return () => {
            window.removeEventListener('popstate', handlePopState);
            if (window.history.state?.youtubePlayerOpen) {
                window.history.back();
            }
        };
    }
    return () => {};
};

useEffect(() => {
    handleYTBackButton(); // Function executes, but return value is ignored
    // No cleanup function is returned to React!
}, [isOpen, onClose]);
```

## The Correct Fix

To make your second approach work, you need to **return the result** of `handleYTBackButton()`:

```javascript
const handleYTBackButton = () => {
    if (isOpen) {
        window.history.pushState({ youtubePlayerOpen: true }, '');
        const handlePopState = () => onClose();
        window.addEventListener('popstate', handlePopState);

        return () => {
            window.removeEventListener('popstate', handlePopState);
            if (window.history.state?.youtubePlayerOpen) {
                window.history.back();
            }
        };
    }
    return () => {};
};

useEffect(() => {
    return handleYTBackButton(); // Return the cleanup function
}, [isOpen, onClose]);
```

## Key Difference

The **cleanup function must be returned from the useEffect callback** for React to properly call it during the cleanup phase. When you call a function inside `useEffect` without returning its result, React has no way to access the cleanup function, so it never gets called when the component unmounts or when dependencies change.