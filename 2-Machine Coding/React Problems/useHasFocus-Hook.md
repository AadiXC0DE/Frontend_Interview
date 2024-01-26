# useHasFocus() Hook in React

## Introduction

The `useHasFocus()` hook in React provides a straightforward way to detect whether a component or element has focus. It encapsulates the logic for tracking focus status and allows components to respond dynamically based on focus state changes.

## useHasFocus() Hook Implementation

Let's implement the `useHasFocus()` hook:

```javascript
import { useState, useEffect } from 'react';

const useHasFocus = (ref) => {
  const [hasFocus, setHasFocus] = useState(false);

  const handleFocus = () => {
    setHasFocus(true);
  };

  const handleBlur = () => {
    setHasFocus(false);
  };

  useEffect(() => {
    const currentRef = ref.current;

    if (currentRef) {
      currentRef.addEventListener('focus', handleFocus);
      currentRef.addEventListener('blur', handleBlur);

      return () => {
        currentRef.removeEventListener('focus', handleFocus);
        currentRef.removeEventListener('blur', handleBlur);
      };
    }
  }, [ref]);

  return hasFocus;
};

export default useHasFocus;
```

## Explanation

1. The `useHasFocus` hook takes a `ref` (component reference).
2. Inside the hook, a state variable `hasFocus` is initialized to track focus status.
3. Event listeners for `focus` and `blur` events are added to the referenced component using `useEffect`.
4. The `handleFocus` and `handleBlur` functions update the `hasFocus` state accordingly.
5. The `useEffect` also removes event listeners when the component unmounts.

## Example Usage in a React Component

```javascript
import React, { useRef } from 'react';
import useHasFocus from './useHasFocus';

const FocusIndicator = () => {
  const inputRef = useRef(null);
  const hasFocus = useHasFocus(inputRef);

  return (
    <div>
      <input ref={inputRef} type="text" />
      {hasFocus ? <p>Input is focused</p> : <p>Input is not focused</p>}
    </div>
  );
};

export default FocusIndicator;
```

## Interview Question

**Possible Interview Question:**
*"Implement a `useHasFocus()` hook in React for detecting focus status of a component or element. Describe the purpose of the hook and how it simplifies tracking focus changes. Provide an example of using the hook in a React component, and discuss scenarios where this hook might be beneficial in a real-world application."*
