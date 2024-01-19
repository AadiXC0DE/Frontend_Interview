# useToggle() Hook in React

## Introduction

The `useToggle()` hook in React simplifies the handling of boolean toggles within components. It provides a straightforward way to manage and toggle between `true` and `false` states.

## useToggle() Hook Implementation

Let's implement the `useToggle()` hook:

```javascript
import { useState } from 'react';

const useToggle = (initialState = false) => {
  const [isToggled, setToggle] = useState(initialState);

  const toggle = () => {
    setToggle((prevToggle) => !prevToggle);
  };

  return { isToggled, toggle };
};

export default useToggle;
```

## Explanation

1. The `useToggle` hook initializes a state variable `isToggled` with an optional default value (default is `false`).
2. The `toggle` function uses the `setToggle` function to invert the current state, effectively toggling between `true` and `false`.

## Example Usage in a React Component

```javascript
import React from 'react';
import useToggle from './useToggle';

const ToggleButton = () => {
  const { isToggled, toggle } = useToggle();

  return (
    <div>
      <button onClick={toggle}>
        {isToggled ? 'ON' : 'OFF'}
      </button>
    </div>
  );
};

export default ToggleButton;
```

## Interview Question

**Possible Interview Question:**
*"Implement a `useToggle()` hook in React for managing boolean toggles within components. Explain the purpose of the hook and how it simplifies the handling of state toggles. Provide an example of using the hook in a React component, and discuss any scenarios where this hook might be beneficial in a real-world application."*

In your response, emphasize the simplicity and clarity that the `useToggle` hook brings to managing toggle state in React components. Discuss scenarios where toggling between `true` and `false` states is a common requirement and how this hook streamlines that process. Consider extensions or modifications based on specific use cases in real-world applications.