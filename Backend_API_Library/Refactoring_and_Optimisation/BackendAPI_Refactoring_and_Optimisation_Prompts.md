# Backend API Refactoring and Optimization Prompts

This document contains a collection of prompts for refactoring and optimizing BackendAPI code, specifically designed for use with LLM assistants like GitHub Copilot.


## Improve the scalability, maintainability, and performance of Java-based REST and GraphQL APIs by refactoring redundant logic, enforcing clean design, and validating changes through robust testing.

### Scenario

Optimize REST/GraphQL API code based on given set of criteria's.

### Prompt

```
//Backend [Specify Language/Framework, e.g., Java /Python etc]: 

Refactor and optimize REST/GraphQL API code to improve maintainability, performance, and code quality. Focus on identifying redundant logic across controllers, resolvers, or service layers and extract reusable functionality into utility or helper methods. Ensure the refactoring adheres to modern API development best practices.

Key Objectives: ( They objectives should be chosen based on focus area for refactoring)

1. **Code Quality & Structure**:
   - Eliminate duplicated logic in request handling, validation, or transformation layers.
   - Extract reusable logic into utility classes or service components.
   - Apply SOLID principles and clean architecture patterns (e.g., controller → service → repository).
   - Improve naming conventions, method signatures, and modularity.
   - Ensure GraphQL resolvers and REST controllers are lean and focused.

2. **API-Specific Optimization**:
   - For REST:
     - Use proper HTTP status codes and response structures.
     - Avoid over-fetching or under-fetching by optimizing DTOs and response models.
   - For GraphQL:
     - Use efficient field resolvers to avoid N+1 query issues.
     - Leverage batching and caching (e.g., DataLoader).
     - Validate schema design for clarity and reusability.

3. **Performance Considerations**:
   - Minimize redundant database or network calls.
   - Use pagination, filtering, and projection to reduce payload size.
   - Optimize serialization/deserialization (e.g., Jackson annotations).
   - Profile endpoints using tools like Spring Actuator, Micrometer, or GraphQL tracing.

4. **Testing & Validation**:
   - Write or update unit and integration tests for refactored logic.
   - Cover edge cases, invalid inputs, and expected outputs.
   - Use tools like JUnit, Mockito, and Spring Test for REST; or graphql-java-test for GraphQL.
   - Ensure backward compatibility of API contracts.

5. **Observability & Error Handling**:
   - Implement consistent error handling using exception mappers or GraphQL error extensions.
   - Add structured logging and correlation IDs for traceability.
   - Integrate with monitoring tools (e.g., Prometheus, Grafana, ELK).

6. **Optional Enhancements**:
   - Add OpenAPI/Swagger documentation for REST endpoints.
   - Use GraphQL schema documentation and introspection features.
   - Refactor large resolvers/controllers into smaller, testable units.

```
----

## Implement consistent and informative error handling.

### Scenario

Basic error handling structure for API endpoints.

### Prompt

```
 Backend [Specify Language/Framework, e.g., Java Spring Boot]: 
 
 Show a try-catch block structure for a service method that might throw a 'ResourceNotFoundException' (custom) or a generic 'DataAccessException'. The catch blocks should log the error and re-throw an appropriate HTTP-status-code-aware exception (e.g., leading to a 404 or 500 response).

```


