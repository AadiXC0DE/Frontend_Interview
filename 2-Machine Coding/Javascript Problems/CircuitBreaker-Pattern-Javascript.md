# Frontend Interview Prep: Circuit Breaker Pattern in JavaScript

## Introduction

The Circuit Breaker Pattern is a design pattern used to prevent cascading failures in distributed systems. While commonly employed in microservices architecture, it can also be valuable in frontend development, especially when making API calls. The main idea is to detect and handle failures gracefully, providing a mechanism to stop further requests for a certain period if a series of failures occurs.

## How Circuit Breaker Works

The Circuit Breaker operates in three states:

1. **Closed State**: In this state, the system operates as usual, and requests are allowed to pass through. If the failure rate is below a certain threshold, the circuit remains closed.

2. **Open State**: If the failure rate exceeds the defined threshold, the circuit breaker transitions to the open state. In this state, requests are blocked, preventing further damage to the system. During this period, no requests are sent to the server.

3. **Half-Open State**: After a specified timeout, the circuit breaker transitions to the half-open state, allowing a limited number of requests to pass through. If these requests are successful, the circuit breaker returns to the closed state. Otherwise, it remains open.

## Circuit Breaker Implementation in JavaScript

Let's implement a simple circuit breaker in JavaScript:

```javascript
class CircuitBreaker {
  constructor(failureThreshold, timeout) {
    this.failureThreshold = failureThreshold;
    this.timeout = timeout;
    this.failureCount = 0;
    this.isOpen = false;
    this.lastFailureTime = null;
  }

  executeRequest(requestFunction) {
    if (this.isOpen) {
      console.log("Circuit is open. Request blocked.");
      return;
    }

    try {
      // Simulate API call
      requestFunction();
      console.log("Request successful.");
    } catch (error) {
      console.error("Request failed:", error);
      this.handleFailure();
    }
  }

  handleFailure() {
    this.failureCount++;

    if (this.failureCount >= this.failureThreshold) {
      this.isOpen = true;
      this.lastFailureTime = Date.now();

      setTimeout(() => {
        this.isOpen = false;
        this.failureCount = 0;
        console.log("Circuit breaker reset. Resuming requests.");
      }, this.timeout);
    }
  }
}

// Example Usage
const circuitBreaker = new CircuitBreaker(3, 5000); // Allow 3 failures in 5 seconds

// Simulate multiple API calls
circuitBreaker.executeRequest(() => { /* API call logic here */ });
```

## Question in an Interview

In an interview, you might be asked to explain the concept of a Circuit Breaker and then implement a simple version in JavaScript. The interviewer may inquire about the key states (closed, open, half-open), failure thresholds, timeouts, and how the system transitions between these states.

**Possible Interview Question:**
*"Can you describe the Circuit Breaker Pattern and implement a basic version in JavaScript? Explain the key states and the purpose of each state in preventing cascading failures during API calls."*