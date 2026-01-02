# Backend API Documentation Prompts

This document contains a collection of prompts for generating documentation for BackendAPI code, specifically designed for use with LLM assistants like GitHub Copilot.


## Quickly create human-readable documentation for API consumers.

### Scenario

Generate a Markdown description for an API endpoint.

### Prompt

```
API Documentation (Markdown): Generate a Markdown section for an API endpoint: 'POST /api/v1/submit-data'.

 Describe its purpose (e.g., "Submits user survey data"), request body (briefly, or refer to a schema), success response (201 Created), and potential error responses (400 Bad Request, 500 Internal Server Error).

```
----

## Prompt for REST API Documentation (Error Handling Focus).

### Scenario

Generate REST API Documentation with focus on Error Handling Details.

### Prompt

```
API Documentation (Markdown):"
Generate detailed documentation for a REST API endpoint that retrieves user data by user ID. Include the HTTP method, endpoint URL, required path and query parameters,
authentication requirements (e.g., bearer token), and example request/response in JSON. Focus extensively on error handling:

-List all relevant HTTP status codes (e.g., 400, 401, 403, 404, 429, 500).
-Describe the cause of each error (e.g., malformed ID, missing token, rate limit exceeded).
-Provide structured JSON examples of error responses.
-Explain how clients should interpret and handle each error.
-Format the documentation in Markdown with clear sections and code blocks."
 
```
----

## Prompt for GraphQL API Documentation (Error Handling Focus).

### Scenario

Generate Graph QL API Documentation with focus on Error Handling Details.

### Prompt

```
API Documentation (Markdown): 

"Generate comprehensive documentation for a GraphQL API query that retrieves user data by ID. Include the query syntax, input argument types, expected response structure,and authentication requirements. Emphasize error handling by covering the following:

-How validation errors (e.g., missing or invalid arguments) are returned.
-How resolver-level errors (e.g., user not found, internal server issues) are represented in the errors array.
-How partial success is handled (e.g., data is returned with errors).
-Include example responses for both full and partial errors.
-Explain how clients should parse and respond to these errors.
-Format the documentation in Markdown with code blocks and clear section headings.
"
 
```
----

## Prompt for REST API Documentation Prompt (Security-Focused).

### Scenario

Generate API Documentation with focus on Security-Focused.

### Prompt

```
API Documentation (Markdown): 

"Generate comprehensive documentation for a REST API endpoint that retrieves user data by user ID. Include the HTTP method, endpoint URL, required path/query parameters, and example request/response in JSON. Focus heavily on security aspects, including:

-Authentication mechanisms (e.g., bearer token, OAuth2).
-Authorization rules (e.g., role-based access, ownership checks).
-Common security concerns (e.g., rate limiting, input validation, injection protection, HTTPS enforcement).
-Detailed error handling for security-related failures (e.g., 401 Unauthorized, 403 Forbidden, 429 Too Many Requests).
-Example headers and secure response formats.
-Format the documentation in Markdown with clear sections, code blocks, and security best practices.
"
```
