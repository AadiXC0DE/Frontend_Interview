# Caching API Response in JavaScript

## Introduction

Caching API responses can significantly improve performance and reduce redundant API calls. In this article, we'll implement a JavaScript function that caches API responses for a given amount of time. This function will be constructed using closures, with an outer function accepting the cache duration and returning an inner asynchronous function for making API calls.

## Caching Function Implementation

Let's create the caching function using closures and helper functions:

```javascript
function createAPICache(cacheDuration) {
  const apiCache = {};

  // Helper function to generate a unique key from arguments
  function generateKey(args) {
    return JSON.stringify(args);
  }

  // Helper function to make a new API call and update the cache
  async function makeAPICallAndCache(key, ...args) {
    const response = await fetch(...args);
    const data = await response.json();
    const expirationTime = Date.now() + cacheDuration;

    apiCache[key] = {
      data,
      expirationTime,
    };

    return data;
  }

  // Inner function to be returned
  return async function cachedAPICall(...args) {
    const key = generateKey(args);

    if (!apiCache[key] || apiCache[key].expirationTime < Date.now()) {
      // Make a new API call if no entry or entry is expired
      return await makeAPICallAndCache(key, ...args);
    } else {
      // Return cached value if the entry is still valid
      console.log("Response from cache");
      return apiCache[key].data;
    }
  };
}

// Example Usage
const cacheDuration = 5000; // Cache responses for 5 seconds
const cachedAPICall = createAPICache(cacheDuration);

// Make API calls
await cachedAPICall('https://api.example.com/data');
await cachedAPICall('https://api.example.com/data'); // Response from cache if within 5 seconds
```

## Explanation

1. The outer function `createAPICache` initializes an empty `apiCache` object to store cached responses.
2. Two helper functions are defined: `generateKey` to create a unique key from the API call arguments and `makeAPICallAndCache` to perform a new API call and update the cache.
3. The inner function returned by `createAPICache` is an asynchronous function `cachedAPICall`. This function generates a key, checks the cache for a valid entry, and either returns the cached data or makes a new API call and updates the cache.

## Interview Question

In an interview, you might be presented with a question like:

**Possible Interview Question:**
*"Implement a JavaScript function that caches API responses for a given duration. Use closures to structure the function. Explain the purpose of the outer and inner functions and describe the role of the helper functions. How would you handle generating unique keys for caching?"*

In your response, emphasize the use of closures, the purpose of each function, the necessity of unique keys for caching, and how the cache expiration is managed.