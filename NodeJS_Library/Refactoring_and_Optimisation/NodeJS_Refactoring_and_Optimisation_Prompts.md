# Node.js Refactoring and Optimization Prompts

This document contains a collection of prompts for refactoring and optimizing Node.js code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Refactor Callbacks to Async/Await](#refactor-callbacks-to-asyncawait)
2. [Optimize a Slow Mongoose Query](#optimize-a-slow-mongoose-query)
3. [Implement Database Connection Pooling](#implement-database-connection-pooling)
4. [Add In-Memory Caching for Frequent Data](#add-in-memory-caching-for-frequent-data)

---

## Refactor Callbacks to Async/Await

### Purpose

Modernize legacy asynchronous code, making it significantly easier to read, debug, and maintain, which is crucial for reducing technical debt in a large codebase.

### Prompt

```
You are an expert Node.js developer specializing in modern JavaScript.

I have a piece of legacy code that uses nested callbacks ("callback hell") for asynchronous operations. Refactor it to use modern async/await syntax.

- Goal: Improve readability and maintainability by flattening the asynchronous logic.
- Error Handling: The refactored code must use a try/catch block to handle errors gracefully, replacing the old if (err) checks.
- Functionality: Ensure the final code maintains the exact same functionality as the original.

Legacy Code to Refactor:
javascript
// [PASTE YOUR NESTED CALLBACK or .then().then() CHAIN CODE HERE]


Provide the fully refactored code using a single async function.
```

**Notes:** In our enterprise repository, finding and eliminating "callback hell" is a high-impact task. This refactoring improves code quality and makes it easier for new developers to understand the logic.

---

## Optimize a Slow Mongoose Query

### Purpose

Get an expert, actionable plan to diagnose and fix slow database queries, a common performance bottleneck in enterprise applications with large datasets.

### Prompt

```
You are an expert in database performance, specifically with MongoDB and Mongoose.

The following Mongoose query is performing slowly under load. Analyze the query and provide a detailed optimization plan.

- 1. Indexing Strategy:
  - Recommend the ideal compound index to support both the filtering (find) and sorting (sort) parts of this query.
  - Explain why this index is effective (e.g., "It follows the ESR rule: Equality, Sort, Range").
- 2. Schema Implementation:
  - Show how to define the recommended index in the Mongoose schema using schema.index(...).
- 3. Query Restructuring:
  - Suggest if the order of fields in the find object should be changed to better match the proposed index.

Slow Mongoose Query:
javascript
// [PASTE YOUR SLOW Mongoose query HERE, e.g., User.find({...}).sort({...})]
```

**Notes:** In our enterprise systems, improper indexing is one of the most frequent causes of performance degradation. This prompt provides a targeted solution that can drastically improve response times for critical APIs.

---

## Implement Database Connection Pooling

### Purpose

Improve database interaction performance and prevent resource exhaustion by implementing connection pooling, a non-negotiable best practice for any production-grade enterprise application.

### Prompt

```
You are an expert in Node.js performance and resource management.

My application is creating a new database connection for every single query, which is inefficient and doesn't scale. Refactor the code to use a centralized connection pool.

- Database: [PostgreSQL (pg) / MySQL (mysql2)]
- Task: Show how to replace individual Client instantiations with a shared Pool instance.
- Provide Code For:
  1. How to initialize and configure the Pool once at application startup.
  2. A refactored function showing how to acquire a client from the pool, execute a query, and release the client back to the pool.

Current Inefficient Code:
javascript
// [PASTE A a function that creates a new DB client instance for a query]
```

**Notes:** Creating new DB connections is resource-intensive. In our high-traffic enterprise environment, not using a pool will lead to performance bottlenecks and can even crash the database server. This is a critical optimization.

---

## Add In-Memory Caching for Frequent Data

### Purpose

Reduce database load and dramatically improve API response times for frequently accessed data by implementing a simple, effective caching layer.

### Prompt

```
You are an expert in application performance and caching strategies.

I have a function that makes a slow database or API call to fetch data that rarely changes. Add an in-memory caching layer to this function to improve performance.

- Library: Use [node-cache / another simple in-memory cache library].
- Task: Refactor the [FUNCTION_NAME] to include caching logic.
- Logic Flow:
  1. First, try to get the data from the cache using a unique key.
  2. If found in the cache (a "cache hit"), return it immediately.
  3. If not found (a "cache miss"), call the original slow function to fetch the data.
  4. Before returning the fresh data, store it in the cache for future requests.

Function to be Optimized:
javascript
// [PASTE THE SLOW function that fetches data, e.g., fetchProductDetails(productId)]
```

**Notes:** This is a classic optimization pattern for our enterprise applications. Caching data like user permissions, application settings, or popular product details can significantly reduce load on downstream systems.
