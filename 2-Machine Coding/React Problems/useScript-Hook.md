# useScript() Hook in React

## Introduction

The `useScript()` hook in React is a custom hook designed to dynamically load external JavaScript files into a React component. This hook simplifies the process of managing script loading, ensuring scripts are loaded only once and providing a way to handle script load events.

## Why it is Needed

Loading external JavaScript files dynamically can be useful in scenarios where you need to load third-party libraries, plugins, or scripts conditionally based on certain conditions or component lifecycle events. The `useScript()` hook abstracts away the complexities of script loading, providing a cleaner and more manageable solution.

## useScript() Hook Implementation

Let's implement the `useScript()` hook:

```javascript
import { useEffect, useState } from 'react';

const useScript = (src) => {
  const [isLoaded, setIsLoaded] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const script = document.createElement('script');
    script.src = src;
    script.async = true;

    const handleLoad = () => {
      setIsLoaded(true);
    };

    const handleError = (error) => {
      setError(error);
    };

    script.addEventListener('load', handleLoad);
    script.addEventListener('error', handleError);

    document.body.appendChild(script);

    return () => {
      script.removeEventListener('load', handleLoad);
      script.removeEventListener('error', handleError);
      document.body.removeChild(script);
    };
  }, [src]);

  return { isLoaded, error };
};

export default useScript;
```

## Explanation

1. The `useScript` hook takes a `src` parameter, representing the URL of the JavaScript file to be loaded.
2. Inside the `useEffect`, a new `<script>` element is created with the provided `src`.
3. Event listeners for `load` and `error` events are added to handle script load success and failure.
4. Upon successful loading, `isLoaded` state is updated to `true`, indicating that the script has been loaded.
5. If an error occurs during script loading, the `error` state is updated with the error message.
6. The hook returns `isLoaded` to indicate whether the script has been loaded and `error` to handle any loading errors.

## Example Usage in a React Component

```javascript
import React from 'react';
import useScript from './useScript';

const MyComponent = () => {
  const { isLoaded, error } = useScript('https://example.com/script.js');

  if (error) {
    return <div>Error: {error.message}</div>;
  } else if (!isLoaded) {
    return <div>Loading...</div>;
  } else {
    return <div>Script is loaded and ready to use!</div>;
  }
};

export default MyComponent;
```

## Interview Question

**Possible Interview Question:**
*"Implement a `useScript()` hook in React for dynamically loading external JavaScript files into a component. Discuss why such a hook might be needed and how it simplifies script loading. Provide an example of using the hook in a React component, and discuss scenarios where this hook might be beneficial in a real-world application."*
