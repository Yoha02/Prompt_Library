# Python Refactoring and Optimisation Prompts

This document contains a collection of prompts for refactoring and optimising Python code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Improve Time Complexity](#improve-time-complexity)
2. [Vulnerability Detection](#vulnerability-detection)
3. [Optimise Memory Usage](#optimise-memory-usage)
4. [Refactor for Maintainability](#refactor-for-maintainability)
5. [Refactor for Scalability](#refactor-for-scalability)
6. [Refactor for Testability](#refactor-for-testability)    

---

## Improve Time Complexity

### Scenario
You have a Python function that performs a specific task correctly, but it suffers from poor performance due to inefficient time complexity. You want to improve its efficiency without changing its output.

### Prompt
```
I have a Python function that works but has poor time complexity. [INSERT FUNCTION HERE]
- Analyze its current time complexity.
- Suggest and implement a more efficient algorithm or data structure.
- Optimize nested loops or redundant operations.
- Add comments explaining the optimization.
- Ensure the output remains the same as the original function.
```
Note: Replace `[INSERT FUNCTION HERE]` with the actual function code.

### Purpose
Improve the performance of an existing Python function by:
- Identifying inefficiencies in its current implementation.
- Applying algorithmic or structural optimizations.
- Maintaining the correctness and output of the original function.
- Making the code more readable and maintainable through comments

---

## Vulnerability Detection

### Scenario
You have a Python codebase that you want to ensure is secure, robust, and maintainable. You're concerned about potential security issues, such as SQL injection, cross-site scripting (XSS), or insecure data handling, logic flaws, and poor coding practices that could lead to bugs or security risks. You want a thorough review to improve the code's quality and safety.

### Prompt
```
Analyze the following Python code for security vulnerabilities: [INSERT CODE HERE]
- Identify potential security risks, such as SQL injection, XSS, or insecure data handling.
- Identify any insecure coding practices (e.g., unsanitized input, hardcoded secrets, unsafe file handling).
- Suggest and implement fixes for identified vulnerabilities.
- Ensure that the code follows best practices for security.
- Add comments explaining the security improvements made.
- Check for improper use of external libraries or APIs.
- Provide recommendations for further security enhancements.
```
Note: Replace `[INSERT CODE HERE]` with the actual code snippet.

### Purpose
To enhance the security of a Python application by:
- Identifying and mitigating potential vulnerabilities.
- Implementing best practices for secure coding.
- Ensuring that the application is robust against common security threats.
- Providing guidance for ongoing security improvements.
- Making the code more secure and resilient against attacks.

---

## Optimise Memory Usage

### Scenario
You have a Python application that consumes a lot of memory, leading to performance issues. The goal is to refactor the code to reduce memory usage while maintaining functionality.

### Prompt
```
Analyze the following Python code for memory usage issues: [INSERT CODE HERE]
- Identify areas where memory consumption can be reduced.
- Suggest and implement optimizations such as using generators, avoiding unnecessary data structures, or using more efficient algorithms.
- Ensure that the functionality of the code remains unchanged.
- Add comments explaining the memory optimizations made.
```
Note: Replace `[INSERT CODE HERE]` with the actual code snippet.

### Purpose
To reduce memory usage in a Python application by:
- Identifying and optimizing memory-intensive operations.
- Implementing efficient data handling techniques.
- Ensuring the application remains functional and efficient.

---

## Refactor for Maintainability

### Scenario
You have a Python codebase that is difficult to maintain due to its structure and complexity. The goal is to refactor the code to improve its maintainability, making it easier for future developers to understand and modify. 

### Prompt
```
Refactor the following Python code to enhance its maintainability: [INSERT CODE HERE]
- Break down large functions into smaller, reusable components.
- Use consistent naming conventions and coding styles.
- Implement design patterns where applicable (e.g., Factory, Singleton).
- Add docstrings and comments to explain the purpose of classes and functions.
- Ensure that the code is modular and follows the Single Responsibility Principle.
- Maintain the original functionality of the code.
```
Note: Replace `[INSERT CODE HERE]` with the actual code snippet you want to refactor.   

### Purpose
To improve the maintainability of Python code by:   
- Making it easier to read and understand.
- Structuring the code for better organization.
- Enhancing the ability to extend and modify the code in the future.

---

## Refactor for Scalability

### Scenario
You have a Python application that works well for small datasets but struggles with larger datasets due to performance issues. The goal is to refactor the code to make it more scalable, allowing it to handle larger inputs efficiently.  

### Prompt
```
Refactor the following Python code to improve its scalability: [INSERT CODE HERE]
- Identify bottlenecks that affect performance with larger datasets.
- Implement more efficient algorithms or data structures.
- Use parallel processing or asynchronous programming where applicable.
- Optimize database queries or external API calls.
- Ensure that the code remains functional and produces the same output.
- Add comments explaining the scalability improvements made.
```
Note: Replace `[INSERT CODE HERE]` with the actual code snippet you want to refactor

### Purpose
To enhance the scalability of a Python application by:
- Improving performance with larger datasets.
- Implementing efficient algorithms and data structures.
- Ensuring that the application can handle increased load without significant performance degradation.
- Making the code more robust and maintainable for future growth.
- Ensuring the application remains functional and responsive under increased load.

---

## Refactor for Testability

### Scenario
You have a Python application that is difficult to test due to tightly coupled components and lack of modularity. The goal is to refactor the code to improve its testability, making it easier to write unit tests and integration tests.  

### Prompt
```
Refactor the following Python code to enhance its testability: [INSERT CODE HERE]
- Identify tightly coupled components and decouple them.
- Use dependency injection to make components more testable.
- Implement interfaces or abstract classes where applicable.
- Ensure that functions and methods have clear inputs and outputs.
- Add docstrings and comments to clarify the purpose of each component.
- Maintain the original functionality of the code.
```
Note: Replace `[INSERT CODE HERE]` with the actual code snippet you want to refactor.

### Purpose
To improve the testability of a Python application by:
- Making it easier to write unit tests and integration tests.
- Structuring the code for better modularity and separation of concerns.
- Ensuring that the application remains functional and maintainable.

---

