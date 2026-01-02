# Node.js Unit Test Generation Prompts

This document contains a collection of prompts for generating unit tests for Node.js applications, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Test an Express.js Route Handler](#test-an-expressjs-route-handler)
2. [Test a Service Layer Function](#test-a-service-layer-function)
3. [Test a Pure Utility Function](#test-a-pure-utility-function)
4. [Test Code with a Mocked Module Dependency](#test-code-with-a-mocked-module-dependency)

---

## Test an Express.js Route Handler

### Purpose

Test the full request/response cycle of an API endpoint, including success and error cases, by isolating the controller from its service dependencies.

### Prompt

```
You are an expert in testing Node.js applications using Jest and Supertest.

Write an integration test suite for an Express.js route handler. The test should mock the service layer to isolate the controller and route logic.

- Setup:
  - Use supertest to make HTTP requests to the Express app instance.
  - Use jest.mock() to mock the [SERVICE_NAME] module.
- Test Scenarios for GET /[RESOURCE]/:id:
  - Success (200): When the mocked service returns a user object, assert that the endpoint responds with a 200 OK status and the correct user data in the body.
  - Not Found (404): When the mocked service returns null, assert that the endpoint responds with a 404 Not Found status.
  - Server Error (500): When the mocked service throws an error, assert that the endpoint responds with a 500 Internal Server Error status.

Code to Test:
typescript
// [PASTE THE Express.js CONTROLLER function and ROUTE setup HERE]


Provide the complete test file [controller_name].test.ts.
```

**Notes:** This is a crucial integration test for any public-facing API in our enterprise. It verifies that routing, request handling, and response formatting work correctly, which is vital for maintaining stable API contracts in our large system.

---

## Test a Service Layer Function

### Purpose

Isolate and verify the business logic within your service layer, ensuring it behaves correctly independent of the database or other external systems.

### Prompt

```
You are an expert in writing unit tests for business logic in TypeScript using Jest.

Write unit tests for a [SERVICE_NAME] method. The tests must mock the repository/database layer to focus solely on the service's logic.

- Setup: Mock the [REPOSITORY_NAME] dependency using jest.fn() for its methods.
- Test Scenarios for [FUNCTION_TO_TEST]:
  - Happy Path: Given valid input (e.g., a DTO), verify that the service correctly calls the repository method with the expected arguments.
  - Data Transformation: If the service maps a DTO to a domain model, assert that the mapping logic is correct.
  - Error Handling: If the repository throws a specific error, verify that the service catches it and re-throws a custom ServiceError or handles it appropriately.

Code to Test:
typescript
// [PASTE THE SERVICE CLASS method HERE]


Provide the complete, focused unit test file for the service.
```

**Notes:** In our multi-layered architecture, testing the service layer in isolation is key. It ensures our core business rules are correct, making the entire system more reliable and easier to refactor.

---

## Test a Pure Utility Function

### Purpose

Ensure the absolute reliability of common, shared utility functions by verifying their correctness against a wide range of inputs and edge cases.

### Prompt

```
You are an expert in writing robust unit tests for pure functions using Jest.

Write a comprehensive test suite for the following utility function. The tests must cover all logical paths and potential edge cases.

- Function to Test: [FUNCTION_SIGNATURE]
- Test Cases:
  - Test with a typical, valid input and assert the expected output.
  - Test with boundary conditions (e.g., empty strings, zero, empty arrays, null/undefined inputs).
  - Test with inputs that trigger different logical branches within the function.

Code to Test:
typescript
// [PASTE THE PURE UTILITY FUNCTION HERE, e.g., a string or date formatter]


Provide a complete test file with multiple test or it blocks, each covering a specific case.
```

**Notes:** Shared utility functions are foundational in our enterprise codebase. A bug in one can have cascading effects across many features. Rigorous testing here is a high-leverage activity for maintaining overall system stability.

---

## Test Code with a Mocked Module Dependency

### Purpose

Isolate units under test from external system interactions (like the file system or network), resulting in fast, reliable, and deterministic tests that can run anywhere.

### Prompt

```
You are an expert in Jest's mocking capabilities.

Write unit tests for a function that depends on an external module (e.g., fs for file system, axios for HTTP requests). The tests must completely mock the external module to prevent actual I/O operations.

- Setup: Use jest.mock('[MODULE_NAME]') to mock the entire external module.
- Test Scenarios:
  - Success Path: Configure the mock implementation (e.g., mockReturnValue, mockResolvedValue) to simulate a successful operation. Verify that your function returns the expected result.
  - Failure Path: Configure the mock to simulate an error (e.g., mockImplementation(() => { throw new Error(...) })). Verify that your function's try/catch block handles the error gracefully.
  - Interaction: Assert that the mocked function was called with the correct arguments using expect(...).toHaveBeenCalledWith(...).

Code to Test:
typescript
// [PASTE THE FUNCTION that uses an external module like 'fs' or 'axios']


Provide the complete test file, including the mock setup.
```

**Notes:** This is essential for any code in our enterprise that interacts with the outside world. Mocking these dependencies is a requirement for true unit testing and is critical for building a fast and stable CI/CD pipeline.
