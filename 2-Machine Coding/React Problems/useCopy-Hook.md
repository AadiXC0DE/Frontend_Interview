# useCopy() Hook in React

## Introduction

The `useCopy()` hook in React is a custom hook designed to simplify the process of copying text to the clipboard. It encapsulates the necessary state and functions for copying, making it easy to integrate into React components.

## useCopy() Hook Implementation

Let's implement the `useCopy()` hook:

```javascript
import { useState } from 'react';

const useCopy = () => {
  const [isCopied, setIsCopied] = useState(false);

  const copyToClipboard = (textToCopy) => {
    navigator.clipboard.writeText(textToCopy)
      .then(() => {
        setIsCopied(true);
        setTimeout(() => setIsCopied(false), 2000); // Reset isCopied after 2 seconds
      })
      .catch((error) => {
        console.error('Copy to clipboard failed:', error);
      });
  };

  return { isCopied, copyToClipboard };
};

export default useCopy;
```

## Explanation

1. The `useCopy` hook initializes a state variable `isCopied` to track whether the text has been successfully copied.
2. The `copyToClipboard` function uses the `navigator.clipboard.writeText()` API to write the specified text to the clipboard.
3. If the copy is successful, `isCopied` is set to `true`, triggering a visual indication. It then resets to `false` after a 2-second timeout.

## Example Usage in a React Component

```javascript
import React from 'react';
import useCopy from './useCopy';

const CopyToClipboardButton = ({ textToCopy }) => {
  const { isCopied, copyToClipboard } = useCopy();

  return (
    <div>
      <button onClick={() => copyToClipboard(textToCopy)}>
        {isCopied ? 'Copied!' : 'Copy to Clipboard'}
      </button>
    </div>
  );
};

export default CopyToClipboardButton;
```

## Interview Question

**Possible Interview Question:**
*"Can you implement a `useCopy()` hook in React for copying text to the clipboard? Explain the purpose of the hook and how it simplifies the process of handling clipboard operations in React components. Provide an example of using the hook in a React component, and discuss any considerations or improvements you might make to this implementation."*

In your response, highlight the purpose of encapsulating clipboard-related functionality into a custom hook, demonstrate the integration of the hook into a React component, and discuss any additional features or error handling considerations that could be implemented. Additionally, be prepared to explain how this hook could be extended or modified based on specific use cases in real-world applications.