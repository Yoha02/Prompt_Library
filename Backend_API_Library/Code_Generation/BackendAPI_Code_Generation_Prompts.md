# Backend API Code Generation Prompts

This document contains a collection of prompts for generating Backend API code, specifically designed for use with LLM assistants like GitHub Copilot.


## Provide a standard way to generate initial bootstrap codebase related to API development.

### Scenario

Generate a full CRUD (Create, Read, Update, Delete) operation codebase using the sample curl/api request as a template.

### Prompt

```
Generate a complete CRUD (Create, Read, Update, Delete) RESTful API codebase for managing product details, using the following detailed requirement : 

Sample Curl: curl -X GET "https://api.example.com/v1/products/12345" \
     -H "Authorization: Bearer YOUR_API_KEY_HERE" \
     -H "Accept: application/json"

Additional Requirements:

Tech Stack:
Language: Python,FastAPI,MongoDB

Endpoints:
POST /products: Create a new product
GET /products/{product_id}: Retrieve product details (as shown in the curl)
PUT /products/{product_id}: Update product details
DELETE /products/{product_id}: Delete a product
GET /products: List all products

Authentication:
Simulate API key authentication using a middleware that checks for a header Authorization: Bearer <API_KEY>.
Use a hardcoded API key for simplicity.
Product Model: Refer attached sample JSON

Extras:
Include basic error handling (e.g., 404 for not found, 401 for unauthorized).
Return JSON responses.
Include example curl commands for each endpoint in comments."

```
----

## Quickly set up the routing and controller structure for a new API.

### Scenario

Generate a basic controller/router for a resource (language-agnostic example, can be tailored).

### Prompt

```
Create a basic controller/router for a 'tasks' resource. Include stubs for functions to handle GET (all tasks), GET (task by ID), POST (new task), PUT (update task), and DELETE (task). Log incoming requests.
```
----

----

## Implement a basic health check endpoint.

### Scenario

Provide a comprehensive and standardized way to monitor API availability and the health of critical dependencies..

### Prompt

```
Create a `/health` GET endpoint that returns a JSON response with detailed health check information. The response should include:


- `status`: Overall API status (e.g., "UP", "DOWN")
- `timestamp`: Current server time in ISO 8601 format
- `uptime`: Duration since the service started
- `version`: API version (e.g., "v1.2.3")
- `dependencies`: An object listing the status of key dependencies (e.g., database, cache, external APIs)

Example response:
{
  "status": "UP",
  "timestamp": "2025-06-12T17:30:00Z",
  "uptime": "72h15m",
  "version": "v1.2.3",
  "dependencies": {
    "database": "UP",
    "redis": "UP",
    "emailService": "DOWN"
  }
}

```
----


## Provide robust, reusable validation for API request payloads.

### Scenario

Define a JSON schema for a complex request body.

### Prompt

```
Create a detailed JSON Schema for a `userProfile` object to be used for validating incoming API requests. The schema should:

1. Define the following fields:
   - `userId`: string, must follow UUID format
   - `firstName`: string, required
   - `lastName`: string, required
   - `email`: string, must follow email format, required
   - `dateOfBirth`: string, must follow date format (YYYY-MM-DD)
   - `address`: object, with the following required fields:
     - `street`: string
     - `city`: string
     - `zipCode`: string or number
     - `country`: string

2. Include:
   - `type` definitions for each field
   - `format` constraints where applicable (e.g., `email`, `uuid`, `date`)
   - `required` fields at both root and nested levels
   - `additionalProperties: false` to enforce strict validation
   - Optional `description` fields for documentation purposes

3. Ensure the schema is compatible with OpenAPI 3.0+ and JSON Schema Draft 7.
```
----

----

## Help developers quickly generate GraphQL schemas and operations from either domain models or existing RESTful API calls (via cURL), enabling faster migration to or integration with GraphQL-based APIs.

### Scenario

Draft a detailed  GraphQL schema for a query based on details provided in terms of context,usecase details etc.

### Prompt

```
Create a GraphQL schema and corresponding query or mutation based on the following context:

1. **Domain Model Scenario**:
   - Define a `Product` type with the following fields:
     - `id`: ID!
     - `name`: String!
     - `description`: String
     - `price`: Float
     - `category`: A nested object with:
       - `id`: ID!
       - `name`: String!
   - Create a `Query` type that allows fetching a `Product` by its `id`.

2. **cURL Command Scenario**:
   - If a cURL command is provided (e.g., `curl -X POST https://api.example.com/products -d '{"name": "Widget"}'`), infer the appropriate GraphQL schema and generate:
     - The relevant `type` definitions
     - A `mutation` or `query` operation that mirrors the intent of the cURL request
     - Input types if needed (e.g., `ProductInput`)
     - Example GraphQL operation (query or mutation) that a developer can run

3. **Validation & Best Practices**:
   - Ensure all required fields are marked with `!`
   - Use meaningful type names and nesting
   - Follow GraphQL naming conventions
   - Include comments or descriptions for each field if possible
4. **Generate GraphQL Resolver, Provider and Service from a given CURL request**:

   - Leverage GQL type and schema while generating resolver, provider, service
```
----

----

## Customize the resource name, schema details, and specific query parameters as needed.

### Scenario

Designing an OpenAPI (Swagger) specification for a new resource.

### Prompt

```
// OpenAPI 3.0: Generate an OpenAPI specification for a '/orders' resource. It should include GET (list all orders, with pagination query parameters 'page' and 'pageSize'), POST (create a new order),

 GET by ID (retrieve a single order), PUT by ID (update an order), and DELETE by ID. Define a basic 'Order' schema with 'orderId', 'customerId', 'orderDate', 'totalAmount', and an array of 'lineItems' (each with 'productId', 'quantity', 'price'). Include standard 400, 404, and 500 error responses.

```
----

----

## Guide the design and documentation of a comprehensive API versioning approach.

### Scenario

Develop a complete API versioning strategy.

### Prompt

```
// Detailed example of handling versioning related aspects of API lifecycle.

// API Design: What are the common strategies for API versioning (URL path, query parameter, custom header)? List pros and cons for each in the context of a large microservices ecosystem.

(Review Copilot's suggestions)

// Based on the [chosen strategy, e.g., URL path versioning like /v1/resource], provide an example of how to implement this in [specific framework, e.g., Express.js or Spring Boot]. Show how routes for v1 and v2 of an '/products' endpoint would look.

// Suggest best practices for communicating API version changes to consumers and managing deprecation of old versions.

```



