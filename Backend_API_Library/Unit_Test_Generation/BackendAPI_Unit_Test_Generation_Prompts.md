# Backend API Unit Test Generation Prompts

This document contains a collection of prompts for generating unit tests for BackendAPI code, specifically designed for use with LLM assistants like GitHub Copilot.


## Automate API endpoint testing.

### Scenario

Generate a test script for an API endpoint (e.g., Postman).

### Prompt

```
Write a comprehensive [Specify the Test framework -Mockio/Postman ]  test script for a GET request to the endpoint `/users/{userId}`. The script should:

1. **Validate HTTP Response:**
   - Assert that the response status code is `200 OK`.
   - Assert that the response time is within acceptable limits (e.g., < 1000ms).
   - Assert that the response body is valid JSON.

2. **Validate Response Schema:**
   - Check that the response contains required fields: `id`, `name`, `email`, `createdAt`.
   - Assert that `responseBody.id` matches the `userId` variable from the Postman environment. (Optinal and specifci to api tool which you are using for testing)

```
----

## Ensure the correctness of backend business logic.

### Scenario

Write a unit test for a service/logic layer function related to a API Backend logic.

### Prompt

```
Backend [Specify Language/Testing Framework, e.g., Python with pytest / Java with Junit/Mockito etc]: 

-Write a pytest unit test for a function 'calculate_discount(price, percentage)'
that returns the discounted price. Include test cases for valid inputs, zero percentage, and 100% percentage. Mock any external dependencies if applicable.

```
