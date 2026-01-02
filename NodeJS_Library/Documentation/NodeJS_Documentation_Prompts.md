# Node.js Documentation Prompts

This document contains a collection of prompts for generating documentation for Node.js applications, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Generate JSDoc for a Middleware Function](#generate-jsdoc-for-a-middleware-function)
2. [Create API Endpoint Documentation in Markdown](#create-api-endpoint-documentation-in-markdown)
3. [Write a "Getting Started" README Section](#write-a-getting-started-readme-section)
4. [Document Environment Variables](#document-environment-variables)

---

## Generate JSDoc for a Middleware Function

### Purpose

Standardize documentation for middleware components, making their purpose, parameters, and side effects immediately clear to anyone reading the code.

### Prompt

```
You are an expert Node.js developer with high standards for code quality.

Generate complete JSDoc documentation for the following Express.js middleware function. The documentation must be clear enough to be used for automated documentation generation.

- Summary: A brief, one-sentence summary of what the middleware does.
- Tags: Include descriptions for the following JSDoc tags:
  - @param {import('express').Request} req - The Express request object.
  - @param {import('express').Response} res - The Express response object.
  - @param {import('express').NextFunction} next - The next middleware function.
- Side Effects: Mention any important side effects, such as "Logs request details to the console" or "Attaches user object to the request."

Code to Document:
javascript
// [PASTE THE JAVASCRIPT/TYPESCRIPT MIDDLEWARE FUNCTION HERE]
```

**Notes:** In a large application with a long chain of middleware, clear JSDoc is essential for debugging and understanding the flow of a request. It's a key part of maintaining a clean and understandable codebase in our enterprise environment.

---

## Create API Endpoint Documentation in Markdown

### Purpose

Quickly generate human-readable API documentation that is essential for front-end teams, QA, and other backend developers who need to interact with your service.

### Prompt

```
You are a technical writer specializing in API documentation.

Generate user-friendly API documentation in Markdown format for the following set of endpoints. The output should be clear and well-structured, suitable for a Postman collection or an internal developer wiki.

- Resource: [RESOURCE_URL] (e.g., /api/v1/tasks)
- For each endpoint, include:
  - Method & Path: e.g., POST /tasks.
  - Description: A brief summary of what the endpoint does.
  - Request Body (if any): A JSON object showing the required fields, types, and if they are optional.
  - Query/Path Parameters (if any): A list of available parameters and their purpose.
  - Success Response: The status code and a sample of the JSON response body.
  - Error Responses: Common error status codes and their meanings.

Endpoint Details:
// [LIST THE ENDPOINTS AND THEIR DETAILS HERE, as shown in the example]

Format the output with clear headings, code blocks, and lists.
```

**Notes:** Maintaining accurate API documentation is a critical process in our enterprise development. This prompt automates the tedious task of formatting, ensuring consistency and clarity for all API consumers across our teams.

---

## Write a "Getting Started" README Section

### Purpose

Provide essential setup instructions to dramatically reduce the time it takes for a new developer to get a project running locally, improving the onboarding experience.

### Prompt

```
You are a developer advocate writing documentation for a new contributor.

Generate a "Getting Started" or "Local Setup" section for a project README.md file. The instructions must be concise, clear, and easy to follow.

- Include Instructions for:
  1. Prerequisites: List required software and versions (e.g., Node.js 18.x, npm/yarn, running MongoDB instance).
  2. Cloning: The git clone command.
  3. Installation: The command to install dependencies (e.g., npm install).
  4. Environment Setup: How to create a .env file from the provided .env.example and what key variables (PORT, DATABASE_URL, JWT_SECRET) need to be set.
  5. Running the App: The command to run the application in development mode (e.g., npm run dev).
  6. Running Tests: The command to run the test suite (e.g., npm test).

Generate the content in Markdown format with numbered steps.
```

**Notes:** A solid "Getting Started" guide is the hallmark of a well-maintained enterprise project. It empowers our new team members to become productive quickly and reduces dependency on other developers for setup help across our organization.

---

## Document Environment Variables

### Purpose

Create clear, centralized documentation for all required environment variables, preventing configuration errors and making it easy to set up the application in different environments (dev, staging, prod).

### Prompt

```
You are a DevOps engineer documenting project configuration.

Generate a Markdown table that documents the required environment variables for this project, based on the .env.example file. This is for the main project README.md.

- Task: Create a table with three columns: "Variable", "Description", and "Example".
- Content: For each variable, provide a clear description of its purpose and an example value (use placeholders for sensitive information).

Variables to Document:

# .env.example contents
PORT=3000
DATABASE_URL=mongodb://localhost:27017/mydb
JWT_SECRET=your-super-secret-key
LOG_LEVEL=info


Generate a clean, well-formatted Markdown table.
```

**Notes:** In our enterprise context with multiple deployment environments, having a single source of truth for configuration variables is critical for both developers and the operations team. This prevents guesswork and deployment failures across our infrastructure.
