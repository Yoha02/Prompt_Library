# Python Documentation Prompts

This document contains a collection of prompts for generating Python documentation, specifically designed for use with LLM assistants like GitHub Copilot.  

## Table of Contents

1. [Project Documentation](#project-documentation)
2. [API Documentation](#api-documentation)
3. [Code Comments](#code-comments)
4. [User Guides](#user-guides)  
5. [Function Documentation](#function-documentation)

---

## Project Documentation

### Scenario
You have a Python project with multiple modules, classes, and functions, and you want to generate clear, structured documentation. This documentation should help developers understand the purpose, usage, and structure of the codebase. You want to automate this process using GitHub Copilot.

### Prompt
```
Generate comprehensive documentation for this Python project. The documentation should include:
- A high-level overview of the project’s purpose and functionality.
- Descriptions for each module, class, and function, including parameters, return types, and usage examples.
- Inline docstrings using the Google or NumPy style guide.
- A README.md file with setup instructions, usage examples, and contribution guidelines.
- Optional: Generate a docs/ folder structure for future expansion (e.g., API reference, tutorials).
- Ensure the documentation is clear, concise, and easy to navigate.
```

### Purpose
To create a well-structured documentation that:
- Provides a clear understanding of the project.
- Helps developers quickly grasp the functionality and usage of the code.
- Facilitates onboarding of new contributors.

---

## API Documentation

### Scenario
You are developing a RESTful API in Python and need to generate documentation that describes the endpoints, request/response formats, and error handling. The goal is to create user-friendly documentation that can be easily understood by developers consuming the API.

### Prompt
```
Generate API documentation for the following Python RESTful API:
- List all endpoints with their HTTP methods (GET, POST, PUT, DELETE).
- Describe the request parameters, including types and whether they are required or optional.
- Provide example requests and responses for each endpoint.
- Include error handling information, such as common error codes and their meanings.
- Use OpenAPI (Swagger) format for the documentation.
- Ensure the documentation is clear, concise, and easy to follow.
``` 
Note: Select actual api code or class to generate the documentation for.

### Purpose
To create comprehensive API documentation that:
- Clearly describes each endpoint and its functionality.
- Provides examples to help developers understand how to interact with the API.
- Includes error handling information to assist in debugging.

---

## Code Comments    

### Scenario
You have a complex Python function or class that needs to be documented with inline comments. The goal is to enhance code readability and maintainability by providing clear explanations of the logic, algorithms, and any complex constructs used.

### Prompt
```
Add inline comments to the following Python code to explain its functionality: [INSERT PYTHON CODE HERE]
- Explain the purpose of each function and class.
- Describe the logic behind complex algorithms or data structures.
- Use comments to clarify any non-obvious parts of the code.
- Ensure the comments are concise and enhance understanding without cluttering the code.
```
Note: Replace `[INSERT PYTHON CODE HERE]` with the actual Python code you want to document.

### Purpose
To improve code readability and maintainability by:
- Providing clear explanations of the code's functionality.
- Clarifying complex logic and algorithms.
- Enhancing understanding for future developers or maintainers.

---

## User Guides

### Scenario
You have developed a Python application that requires user documentation. The goal is to create a user guide that explains how to install, configure, and use the application effectively. The guide should be easy to follow and include troubleshooting tips.

### Prompt
```
Create a user guide for the following Python application: [INSERT APPLICATION NAME HERE]
The guide should include:
- Installation instructions, including prerequisites and dependencies.
- Configuration steps, if applicable.
- A step-by-step tutorial on how to use the application.
- Common use cases and examples.
- Troubleshooting tips for common issues.
- A FAQ section addressing common questions.
- Ensure the guide is well-structured, easy to read, and includes screenshots or diagrams where appropriate.
``` 
Note: Replace `[INSERT APPLICATION NAME HERE]` with the actual name of the application.

### Purpose
To create a user-friendly guide that:
- Helps users install and configure the application.
- Provides clear instructions on how to use the application effectively.
- Addresses common issues and questions to enhance user experience.

---

## Function Documentation

### Scenario
You have a Python function that performs a specific task, and you want to generate documentation that describes its purpose, parameters, return values, and usage examples. The goal is to create clear and concise documentation that can be easily understood by other developers.

### Prompt
```
Document the following Python function: [INSERT FUNCTION NAME HERE]
- Add a docstring that describes the function's purpose.
- List all parameters with their types and whether they are required or optional.
- Describe the return value, including its type and meaning.
- Provide usage examples to illustrate how the function can be used.
- Ensure the documentation follows the Google or NumPy style guide.
``` 
Note: Replace `[INSERT FUNCTION NAME HERE]` with the actual function you want to document.

### Purpose
To create clear and concise documentation for a Python function that:
- Describes its purpose and functionality.
- Lists parameters and return values in a structured format.
- Provides usage examples to help developers understand how to use the function effectively.

---
