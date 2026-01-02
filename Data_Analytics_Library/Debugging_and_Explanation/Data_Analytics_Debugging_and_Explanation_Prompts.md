# Data and Analytics Debugging and Explanation Prompts

This document contains a collection of prompts for debugging and explaining Data and Analytics code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Debuggin Data Processing Errors](#debugging-data-processing-errors)
2. [Debugging API Integration Failures](#debugging-api-integration-failures)
3. [Explain Code Logic for Business Rules](#explain-code-logic-for-business-rules)
4. [Debugging Performance Bottlenecks](#debugging-performance-bottlenecks)
5. [Explain Error Handling Logic](#explain-error-handling-logic)

---

## Debugging Data Processing Errors

### Purpose

To resolve issues in data workflows and ensure accurate processing.

### Prompt

```
Identify and debug issues in data processing workflows:

- Trace errors in ETL pipelines, such as missing or corrupted data.

- Debug SQL queries to identify incorrect joins, filters, or aggregations.

- Provide a step-by-step explanation of the root cause and suggest fixes.
```

**Notes:** Keep the selection of the code while sending this prompt.

---

## Debugging API Integration Failures

### Purpose

Understand the root cause of a critical ANR freeze, pinpoint the exact problematic code from a system trace, and To fix API-related issues and improve integration reliability.

### Prompt

```
Debug API integration issues in your systems:

- Investigate failed API requests due to timeouts, invalid responses, or authentication errors.

- Explain the cause of the failure and provide recommendations for retries or error handling.

- Suggest improvements to ensure robust API communication.
```

**Notes:** 

---

## Explain Code Logic for Business Rules

### Purpose

To help developers understand and improve business-critical code.

### Prompt

```
Analyze and explain the logic behind business rule implementation:

- Break down complex functions or algorithms used for calculations.

- Provide a detailed explanation of how the code handles edge cases and exceptions.

- Suggest optimizations or refactoring for better clarity and performance.
```

**Notes:** Make sure co-pilot knows what code you are referring to by selecting it in your active document within Visual Studio Code or paste the code snippet into your query.

---

## Debugging Performance Bottlenecks

### Purpose

To improve the speed and efficiency of data workflows and queries.

### Prompt

```
Identify and debug performance bottlenecks in [SQL / DAG / SCRIPT]:

- Analyze slow-running SQL queries or data processing scripts.

- Explain the cause of the bottleneck, such as inefficient joins or lack of indexing.

- Provide recommendations to optimize performance and scalability.
```

**Notes:** Provide the context of which SQL, Python code or any DAG you are referring to.

---

## Explain Error Handling Logic

### Purpose

To ensure error handling is clear, effective, and aligned with your organization's operational standards.

### Prompt

```
Analyze and explain the error handling logic in the code:

- Identify how the code handles exceptions, retries, and logging.

- Provide a detailed explanation of the flow when errors occur.

- Suggest improvements to make error handling more robust and user-friendly.
```

**Notes:** Make sure co-pilot knows what code you are referring to by selecting it in your active document within Visual Studio Code or paste the code snippet into your query.
