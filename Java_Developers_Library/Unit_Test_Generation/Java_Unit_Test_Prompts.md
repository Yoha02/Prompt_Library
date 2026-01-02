# Unit Testing Prompts

## Basic Unit Test
### Use Case  
Create a JUnit 5 test for a method, ensuring edge case coverage, meaningful assertions, and proper setup.

### Prompt  
Write a JUnit 5 test for this method.

---

## Parameterized Tests
### Use Case  
Generate JUnit 5 test cases for a Java method using `@ParameterizedTest` and `@CsvSource`.

### Prompt  
The method should take multiple input arguments and return a computed result.  
Include cases that validate both expected functionality and potential failure scenarios.  
Generate a JUnit test for this method with multiple inputs.

---

## Mocking with Mockito
### Use Case  
Develop a JUnit 5 test with Mockito, mocking dependencies and verifying interactions.

### Prompt  
- Use `Mockito.verify()` to validate interactions.  
- Handle edge cases and create assertions for them.  
Write a test using Mockito for this service method.

---

## Exception Testing
### Use Case  
Validate if a method handles exceptions properly using JUnit 5.

### Prompt  
Write a JUnit 5 test to validate if the method handles `NullPointerException` using `assertThrows`.  
Verify exception handling, error messages, and ensure proper business logic compliance.  
Create a test method to validate if the method handles `NullPointerException`.

---

## Mocking Static Methods
### Use Case  
Test static methods using Mockito in JUnit 5.

### Prompt  
Use `Mockito.mockStatic()` to mock static methods effectively.  
Ensure correct behavior verification and cleanup using try-with-resources.  
Test a static method using Mockito.

---

## Integration Testing
### Use Case  
Create a JUnit 5 integration test for a Spring Boot application.

### Prompt  
Use `@SpringBootTest` to configure the application context properly.  
Mock dependencies and verify endpoint responses.  
Write an integration test for this Spring Boot controller.

---

## Assertions & Test Validation
### Use Case  
Enhance test validations using JUnit 5 assertions.

### Prompt  
Use `Assertions.assertEquals`, `assertTrue`, and `assertAll` for better result clarity and grouping assertions together.  
Use assertions to validate test outcomes.