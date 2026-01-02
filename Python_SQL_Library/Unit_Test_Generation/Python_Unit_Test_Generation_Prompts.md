# Python Unite Test Generation Prompts

This document contains a collection of prompts for generating unit tests for Python code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Generate Unit Tests](#generate-unit-tests)
2. [Test Edge Cases](#test-edge-cases)
3. [Mocking and Stubbing](#mocking-and-stubbing)
4. [Test Coverage](#test-coverage)  
5. [Test Data Generation](#test-data-generation)

---

## Generate Unit Tests

### Scenario
You have a Python function or module that you want to test. The goal is to generate comprehensive unit tests that cover various scenarios, including use cases, and error handling. You want to ensure that the tests are well-structured, easy to read, and follow best practices.  

### Prompt
```
Generate unit tests for the following Python function/module: [INSERT FUNCTION OR MODULE HERE]
- Include tests for normal cases, and error handling.
- Use assertions to verify expected outputs.
- Use the unittest or pytest framework.
- Ensure that the tests are well-structured and easy to read.
- Add comments explaining the purpose of each test.
- Use mock objects where necessary to isolate the function/module being tested.
- Ensure that the tests can be run independently and do not rely on external state.
- Be organized in a separate test_*.py file or test class.
```
Note: Replace `[INSERT FUNCTION OR MODULE HERE]` with the actual function or module code.

### Purpose
To create a comprehensive suite of unit tests that:
- Validates the functionality of the Python code.
- Covers a wide range of scenarios, including edge cases.
- Ensures that the code behaves as expected under various conditions.
- Follows best practices for test structure and readability.

---

## Test Edge Cases

### Scenario
You have a Python function that needs to be tested for edge cases. The goal is to identify potential edge cases and generate tests that ensure the function behaves correctly under these conditions. You want to ensure that the function handles unusual or extreme inputs gracefully.

### Prompt
```
Identify and test edge cases for the following Python function: [INSERT FUNCTION HERE]
- List potential edge cases that could affect the function's behavior.
- Generate unit tests for each identified edge case.
- Ensure that the tests cover both valid and invalid edge cases.
- Use the unittest or pytest framework.
- Add comments explaining the purpose of each edge case test.
- Ensure that the function handles edge cases gracefully without crashing or producing incorrect results.
```
Note: Replace `[INSERT FUNCTION HERE]` with the actual function code.

### Purpose
To ensure that the Python function is robust and reliable by:
- Identifying and testing edge cases that could lead to unexpected behavior.
- Validating that the function handles these cases correctly.
- Enhancing the overall reliability and stability of the code.

---

## Mocking and Stubbing

### Scenario
You have a Python function that interacts with external systems (e.g., databases, APIs) and you want to test it without relying on these external systems. The goal is to use mocking and stubbing to isolate the function and test its behavior independently.

### Prompt
```
Generate unit tests for the following Python function using mocking and stubbing: [INSERT FUNCTION HERE]
- Use the unittest.mock library to create mock objects for external dependencies.
- Ensure that the tests do not rely on actual external systems.
- Validate the function's behavior with mocked responses.
- Include tests for both normal cases and error handling.
- Add comments explaining the purpose of each test and the use of mocks.
- Ensure that the tests can be run independently and do not require external resources.
```
Note: Replace `[INSERT FUNCTION HERE]` with the actual function code.   

### Purpose
To test the Python function in isolation by:
- Using mocks to simulate external dependencies.
- Ensuring that the function behaves correctly without relying on external systems.
- Validating the function's logic and error handling independently.

---

## Test Coverage

### Scenario
You have a Python codebase and want to ensure that your unit tests provide adequate coverage. The goal is to analyze the test coverage and generate additional tests if necessary to cover untested code paths.

### Prompt
```
Analyze the test coverage for the following Python codebase: [INSERT CODEBASE HERE]
- Use a coverage analysis tool (e.g., coverage.py) to identify untested code paths
- Generate additional unit tests to cover the uncovered code paths.
- Ensure that the new tests are well-structured and follow best practices.
- Add comments explaining the purpose of each new test.
- Validate that the tests improve overall coverage without duplicating existing tests.
```
Note: Replace `[INSERT CODEBASE HERE]` with the actual codebase or specific files you want to analyze.

### Purpose
To ensure that the Python codebase has adequate test coverage by:
- Identifying untested code paths.
- Generating additional tests to cover these paths.
- Improving the reliability and robustness of the code through comprehensive testing.

---

## Test Data Generation

### Scenario
You have a Python function that requires specific input data for testing. The goal is to generate realistic test data that covers a wide range of scenarios, including normal cases, edge cases, and error conditions.

### Prompt
```
Generate realistic test data for the following Python function: [INSERT FUNCTION HERE]
- Identify the input parameters and their expected data types.
- Create a variety of test data that covers normal cases, edge cases, and error conditions.
- Ensure that the test data is diverse and representative of real-world scenarios.
- Include comments explaining the purpose of each test data set.
- Validate that the function behaves correctly with the generated test data.
```
Note: Replace `[INSERT FUNCTION HERE]` with the actual function code.

### Purpose
To create realistic and comprehensive test data for the Python function by:
- Covering a wide range of scenarios, including edge cases.
- Ensuring that the function can handle various inputs correctly.
- Enhancing the reliability and robustness of the tests through diverse data sets.

---

