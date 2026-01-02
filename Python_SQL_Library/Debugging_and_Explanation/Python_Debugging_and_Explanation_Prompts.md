# Python Debugging and Explanation Prompts

This document contains a collection of prompts for debugging and explaining Python code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Debugging Python Code](#debugging-python-code)
2. [Explaining Python Code](#explaining-python-code)
3. [Error suppression and Logging](#error-handling-and-logging)
4. [Error Handling and Logging](#error-handling-and-logging)

---

## Debugging Python Code

### Scenario
You have a Python script that is not functioning as expected. The goal is to identify and fix the issues in the code, ensuring it runs correctly and efficiently. e.g. You’re encountering a NoneType (null pointer) error in a Python function, which is likely caused by an unexpected None value being used in an operation. You want to debug the issue, prevent it from recurring, and make the function more robust against similar problems in the future.

### Prompt
```
I'm getting a NoneType (null pointer) or [Error Information] error in this Python function.
- Identify which variable is None and causing the error.
- Add appropriate checks to prevent operations on None values.
- Suggest default values or fallback logic where needed.
- Add logging or print statements to trace variable values before the error occurs.
- Ensure the function handles unexpected None inputs gracefully.
- Provide a revised version of the function with these improvements.
```
Note: Replace `[Error Information]` with the specific error message you are encountering.

### Purpose
To debug and improve the reliability of a Python function by:
- Identifying the root cause of a NoneType error.
- Adding safeguards and fallback mechanisms.
- Enhancing traceability with logging or print statements.
- Ensuring the function behaves predictably even with incomplete or unexpected input.

---

## Explaining Python Code

### Scenario
You have a piece of Python code that you need to understand better. The goal is to break down the code into understandable parts, explaining its functionality, logic, and any complex constructs used.

### Prompt
```
Explain the following Python code step-by-step:
- Break down the code into logical sections.
- Explain the purpose of each section and how it contributes to the overall functionality.
- Describe any complex constructs or algorithms used.
- Provide examples of input and output for better understanding.
``` 
Note: Replace the code snippet with the actual Python code you want to explain.

### Purpose
To provide a clear and detailed explanation of Python code by:
- Breaking down complex logic into manageable parts.
- Clarifying the purpose and functionality of each section.
- Offering examples to illustrate how the code works in practice.

---

## Error Suppression and Logging

### Scenario
You have a Python application that needs better error suppression and logging practices. The goal is to implement robust error handling mechanisms and logging practices to improve the application's reliability and traceability.

### Prompt
```
Improve the error suppression and logging in the following Python code:
- Identify potential failure points and add appropriate try-except blocks to suppress errors.
- Implement custom exception classes where necessary.
- Use logging instead of print statements for better traceability.
```
Note: Replace the code snippet with the actual Python code you want to enhance.

### Purpose
To enhance the reliability and traceability of a Python application by:
- Implementing robust error suppression mechanisms.
- Using logging practices instead of print statements.
- Providing informative error messages for better debugging.

---

## Error Handling and Logging

### Scenario
You have a Python application that needs better error handling and logging. The goal is to implement robust error handling mechanisms and logging practices to improve the application's reliability and traceability.

### Prompt
```
Improve the error handling and logging in the following Python code:
- Identify potential failure points and add appropriate try-except blocks.
- Implement custom exception classes where necessary.
- Use logging instead of print statements for better traceability.
- Ensure that error messages are informative and actionable.
- Provide a revised version of the code with these improvements.
```
Note: Replace the code snippet with the actual Python code you want to enhance.

### Purpose
To enhance the reliability and traceability of a Python application by:
- Implementing robust error handling mechanisms.
- Using logging practices instead of print statements.
- Providing informative error messages for better debugging.    

---
