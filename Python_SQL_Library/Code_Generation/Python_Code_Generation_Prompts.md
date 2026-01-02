# Python Code Generation Prompts

This document contains a collection of prompts for generating Python code, specifically designed for use with LLM assistants like GitHub Copilot.


## Table of Contents

1. [Implement Restful APIs](#implement-restful-apis)
2. [Build Business Logic](#build-business-logic)
3. [Create Jupyter Notebook](#create-jupyter-notebook)
4. [Model Conversion](#model-conversion)
5. [Build python Project](#build-python-project)

---

## Implement Restful APIs

### Scenario
you are developing a RESTful API in Python to manage a "Product" resource. The API should support full CRUD functionality, enforce business rules, validate input, and provide useful operational features like logging and reporting. You want to use FastAPI or Flask and keep the implementation simple with an in-memory data store.

### Prompt
```
Create a RESTful API using FastAPI (or Flask) in Python with the following features:
Endpoints for CRUD operations on a "Product" resource (id, name, price, quantity).
Business logic to:
- Prevent creation of products with negative price or quantity.
- Automatically apply a 10% discount if quantity > 100.
- Return a summary report endpoint that calculates total inventory value.
- Use Pydantic models for request validation.
- Include error handling for invalid input and missing resources.
- Add logging for each request and response.
- Optionally, use an in-memory store (like a dictionary) for simplicity.
- Ensure the API is well-documented with OpenAPI specifications.
```
Note: Update the Restful APIs requrements as needed to fit your specific use case.

### Purpose
To build a lightweight, well-structured RESTful API that:
- Demonstrates clean API design with FastAPI or Flask.
- Enforces business rules and input validation.
- Provides useful operational insights (like inventory value).
- Is easy to test and extend, using in-memory storage and logging.

---

## Build Business Logic

### Scenario
You have a specific business requirement that needs to be translated into Python code. The goal is to generate clean, maintainable, and well-documented code that aligns with the requirement while leaving room for future enhancements.

### Prompt
``` 
Generate Python code based on the following business requirement: [INSERT BUSINESS REQUIREMENT HERE]
The code should:
- Follow clean coding practices and be easy to understand.
- Include comments explaining each major step.
- Use appropriate data structures and error handling.
- Include a placeholder comment where additional business logic can be added.
- Be modular and reusable if possible.
- Ensure that the code is testable and can be easily integrated with unit tests.
```
Note: Replace `[INSERT BUSINESS REQUIREMENT HERE]` with the specific business requirement you want to implement.

### Purpose
To create a Python implementation that:
- Accurately reflects the business requirement.
- Is easy to read, maintain, and extend.
- Demonstrates good software engineering practices.
- Provides a solid foundation for future development

---

## Create Jupyter Notebook

### Scenario
You have to build a Jupyter notebook for POC (Proof of Concept) that demonstrates a specific functionality or data analysis task. The notebook should be well-structured, with clear explanations and visualizations.

### Prompt
```
Create a Jupyter notebook that demonstrates the following functionality: [INSERT FUNCTIONALITY OR DATA ANALYSIS TASK HERE]
The notebook should:
- Start with a brief introduction explaining the purpose of the notebook.
- Include necessary imports and setup code.
- Provide clear, step-by-step explanations of each code block.
- Use comments to explain complex logic or calculations.
- Ensure that the notebook is well-organized with markdown cells for explanations.
```
Note: Replace `[INSERT FUNCTIONALITY OR DATA ANALYSIS TASK HERE]` with the specific task you want to demonstrate.

### Purpose
To create a Jupyter notebook that:
- Effectively demonstrates a specific functionality or data analysis task.
- Is easy to follow and understand.
- Provides a clear and structured approach to the task.

---

## Model Conversion

### Scenario
You need to convert a json schema into Python data models using Pydantic. The goal is to create models that are easy to use, validate, and extend.

### Prompt
```
Generate Python data models using Pydantic based on the following JSON schema: [INSERT JSON SCHEMA HERE]
The models should:
- Include all necessary fields with appropriate types.
- Implement validation rules as specified in the schema.
- Use Pydantic's features for data validation and serialization.
- Be modular and reusable.
- Include comments explaining each model and its fields.
```
Note: Replace `[INSERT JSON SCHEMA HERE]` with the specific JSON schema you want to convert into Pydantic models.

### Purpose
To create Pydantic data models that:
- Accurately reflect the structure and validation rules of the JSON schema.
- Are easy to use and integrate into Python applications.
- Provide a solid foundation for data validation and serialization in Python applications.

---

## Build Python Project

### Scenario
You are starting a new Python project and want to follow the Model-View-Controller (MVC) design pattern. To ensure maintainability and clarity, you need a clean and well-documented boilerplate structure that separates concerns across models, views, and controllers, with a clear entry point to run the application

### Prompt
```
Generate a boilerplate Python project structure using the MVC (Model-View-Controller) design pattern. The structure should include:
- A models module for data classes or database interaction.
- A views module for user interface or output formatting (CLI or web-based).
- A controllers module to handle business logic and coordinate between models and views.
- An app.py or main.py entry point to initialize and run the application.
- Use clean code practices and include comments explaining each component.
- Add placeholder methods in each module to demonstrate the flow of data and control.
- Ensure the project is easy to extend with additional features in the future.
```

### Purpose
To create a reusable and well-organized Python project scaffold that:
- Follows the MVC design pattern for separation of concerns.
- Serves as a starting point for scalable application development.
- Demonstrates the interaction between components through placeholder logic.
- Promotes clean code and maintainability with clear documentation.

---
