# Node.js Code Generation Prompts

This document contains a collection of prompts for generating Node.js code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Generate a Full CRUD Express.js Router](#generate-a-full-crud-expressjs-router)
2. [Generate a Mongoose Schema and Model](#generate-a-mongoose-schema-and-model)
3. [Generate a Generic Service Layer](#generate-a-generic-service-layer)
4. [Generate a JWT Authentication Middleware](#generate-a-jwt-authentication-middleware)

---

## Generate a Full CRUD Express.js Router

### Purpose

Quickly scaffold a complete and well-structured set of RESTful endpoints for a new resource, including essential validation and error handling patterns.

### Prompt

```
You are an expert Node.js developer specializing in Express.js and TypeScript.

Generate a complete Express.js router for a [RESOURCE_NAME] resource (e.g., 'products').

- File Structure: Create the code for a new file named [RESOURCE_NAME].routes.ts.
- Routes (CRUD):
  - GET /[RESOURCE_PLURAL]: List all resources.
  - GET /[RESOURCE_PLURAL]/:id: Get a single resource by ID.
  - POST /[RESOURCE_PLURAL]: Create a new resource.
  - PUT /[RESOURCE_PLURAL]/:id: Update an existing resource.
  - DELETE /[RESOURCE_PLURAL]/:id: Delete a resource.
- Validation: Use express-validator for the POST and PUT routes to validate the request body (e.g., [FIELD_1] is a required string, [FIELD_2] is a required number).
- Handler Logic: Each route handler must be an async function that:
  1. Calls a placeholder service function (e.g., [RESOURCE_NAME]Service.create(...)).
  2. Includes try/catch for robust error handling, sending a 500 response on failure.
  3. Sends an appropriate JSON response on success.

Provide only the final, complete code for the router file.
```

**Notes:** Specify the resource name and the fields to be validated. This prompt assumes a service layer ([RESOURCE_NAME]Service) exists to abstract the database logic, which is a common and recommended architectural pattern in our enterprise applications.

---

## Generate a Mongoose Schema and Model

### Purpose

Efficiently define a complete data model for MongoDB interactions, including validation, defaults, middleware hooks for business logic, and virtual properties for computed data.

### Prompt

```
You are an expert in MongoDB and Mongoose with TypeScript.

Generate a Mongoose schema and model for a [MODEL_NAME] collection (e.g., 'User').

- Schema Fields: Define the following fields with appropriate types and validation:
  - [FIELD_1_NAME]: e.g., String, required, unique, trim.
  - [FIELD_2_NAME]: e.g., String, required, match (regex), lowercase.
  - [FIELD_3_NAME]: e.g., Date, default Date.now.
  - [FIELD_4_NAME]: e.g., Array of Strings, enum, with a default value.
- Middleware Hooks: Add a pre-save hook that automatically updates an updatedAt field whenever the document is modified.
- Virtual Properties: Define a virtual property (e.g., fullName) that combines two other fields (e.g., firstName and lastName).
- Export: Export the compiled Mongoose model.

Provide only the final code for the Mongoose schema and model file.
```

**Notes:** This prompt creates more than just a data structure; it builds a "smart" model with built-in business rules, which is crucial for maintaining data integrity in our large application ecosystem.

---

## Generate a Generic Service Layer

### Purpose

Quickly scaffold a clean and testable service layer that abstracts data access logic, separates concerns, and uses DTOs to define clear API contracts.

### Prompt

```
You are an expert Node.js architect specializing in TypeScript.

Generate a service class that abstracts database operations for a [MODEL_NAME] resource, using a conceptual Repository Pattern.

- Assumption: Assume a generic Repository<T> class already exists with methods like create(item: T), findById(id: string), etc.
- Service Class ([MODEL_NAME]Service):
  - It should be instantiated with a Repository<[MODEL_NAME]>.
  - Implement CRUD methods like create[MODEL_NAME], get[MODEL_NAME]ById, update[MODEL_NAME], and delete[MODEL_NAME].
- DTOs & Mapping: The create and update methods must accept Data Transfer Objects (DTOs) (e.g., Create[MODEL_NAME]Dto) and handle the mapping logic from DTO to the domain model before calling the repository.
- Error Handling: Include basic error handling in each method (e.g., log errors and re-throw them as custom service-level errors).

Provide only the code for the service class and its required DTOs.
```

**Notes:** The Service/Repository pattern is fundamental for building scalable and maintainable backends in our enterprise. It decouples our business logic (Service) from our data access implementation (Repository), making our applications more testable and adaptable.

---

## Generate a JWT Authentication Middleware

### Purpose

Generate standard, secure authentication middleware for protecting API routes, ensuring all necessary checks and error responses are handled correctly.

### Prompt

```
You are an expert in Node.js security.

Generate an Express.js middleware function in TypeScript for JWT authentication.

- Function Name: authenticateJwt
- Behavior:
  1. Extract the JWT from the Authorization header (must support the "Bearer [token]" scheme).
  2. If no token is provided, respond immediately with a 401 Unauthorized error.
  3. Use the jsonwebtoken library to verify the token against a secret from process.env.JWT_SECRET.
  4. If verification fails (e.g., invalid signature, expired token), respond with a 403 Forbidden error.
  5. If successful, attach the decoded payload to the req.user property and call next() to pass control to the next handler.

Provide only the code for the authentication middleware function.
```

**Notes:** This is a core component of almost any modern web application in our enterprise. Having a robust, standardized prompt for it saves our team time and reduces the risk of security mistakes across our projects.
