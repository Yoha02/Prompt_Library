# Node.js Debugging and Explanation Prompts

This document contains a collection of prompts for debugging and explaining Node.js concepts, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Explain "Cannot read property '...' of undefined"](#explain-cannot-read-property--of-undefined)
2. [Explain the Node.js Event Loop](#explain-the-nodejs-event-loop)
3. [Debug an Unresolved Promise or async Function](#debug-an-unresolved-promise-or-async-function)
4. [Explain and Fix a CORS Error](#explain-and-fix-a-cors-error)

---

## Explain "Cannot read property '...' of undefined"

### Purpose

Understand and fix one of the most common runtime errors in JavaScript, learning defensive coding practices that are essential for building resilient applications.

### Prompt

```
You are an expert Node.js debugger.

I am getting a TypeError: Cannot read property '[PROPERTY_NAME]' of undefined in my application. Analyze the provided code block and explain the issue.

- Identify Common Causes: Explain why this error typically occurs in JavaScript (e.g., an object is null or undefined when one of its properties is accessed).
- Pinpoint the Problem: In the given code, identify the specific variable that is likely undefined.
- Provide Solutions:
  - Show how to fix the issue using defensive coding techniques like optional chaining (?.) or explicit if checks.
  - Suggest debugging steps (e.g., using console.log or a debugger breakpoint) to inspect the variable's value at runtime.

Problematic Code:
javascript
// [PASTE THE CODE BLOCK where the TypeError occurs]
```

**Notes:** This error is frequent but often indicates a deeper issue with data flow or assumptions in our code. Building robust checks is a core discipline for writing enterprise-grade software that can handle unexpected API responses or data states.

---

## Explain the Node.js Event Loop

### Purpose

Clarify fundamental Node.js architectural concepts, helping developers write more efficient, non-blocking code and understand the performance characteristics of the platform.

### Prompt

```
You are an expert in Node.js architecture.

Explain the Node.js event loop and the concept of non-blocking I/O in simple, clear terms.

- Core Concepts:
  - What is the event loop and what is its primary responsibility?
  - How does non-blocking I/O work, and how does it allow Node.js to handle many concurrent connections efficiently with a single thread?
- Provide a Code Example:
  - Write a small code snippet that demonstrates a non-blocking operation (e.g., using setTimeout or fs.readFile).
  - Explain, step-by-step, how the event loop processes this code, including the role of the call stack and the callback queue.

Keep the explanation concise and easy for a mid-level developer to understand.
```

**Notes:** A deep understanding of the event loop is a differentiator for senior backend engineers in our enterprise. It's critical for diagnosing performance bottlenecks and designing highly concurrent systems capable of handling our enterprise-level traffic.

---

## Debug an Unresolved Promise or async Function

### Purpose

Troubleshoot common but frustrating issues in asynchronous code, ensuring that Promises resolve correctly and data flows as expected through your application.

### Prompt

```
You are an expert in debugging asynchronous JavaScript.

My async function is not working as expected. It's either returning undefined immediately or the Promise it returns never seems to resolve.

- Analyze Common Mistakes: Based on the provided code, identify common pitfalls with async/await and Promises that could be causing this issue, such as:
  - A missing return statement inside the try block.
  - Not await-ing an asynchronous operation.
  - Calling a function that does not actually return a Promise.
  - An unhandled rejection in a .then() chain.
- Suggest Debugging Steps:
  - Recommend how to debug the promise flow, such as adding console.log statements at different stages or using the debugger's "step over" functionality to trace the execution path.

Problematic async Function:
javascript
// [PASTE YOUR ASYNC FUNCTION that is not resolving correctly]
```

**Notes:** Asynchronous logic is at the heart of our Node.js applications. Flaws in promise handling can lead to silent failures and hard-to-diagnose bugs, making mastery of this topic essential for application stability in our complex enterprise system.

---

## Explain and Fix a CORS Error

### Purpose

Understand and resolve common CORS errors that occur when developing separate front-end and back-end applications, a standard practice in modern web architecture.

### Prompt

```
You are an expert in web security and Express.js.

My front-end application (running on [FRONTEND_URL]) is getting a CORS (Cross-Origin Resource Sharing) error when trying to make an API request to my Node.js backend.

- Explain the Error: In simple terms, explain what a CORS error is and why browsers enforce this security policy.
- Provide the Solution:
  - Show how to fix this by using the cors middleware package in my Express.js application.
  - Provide the code to configure the middleware to only allow requests from my specific front-end origin ([FRONTEND_URL]).
  - Explain how to configure it to support credentials (credentials: true) and specific HTTP methods if needed.

Provide the necessary npm install command and the Express.js server setup code.
```

**Notes:** Properly configuring CORS is a security requirement for our enterprise applications with web-based front-ends. A misconfiguration can either block legitimate traffic or, worse, open up security vulnerabilities across our services.
