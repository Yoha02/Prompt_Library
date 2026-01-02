# Data & Analytics Documentation Prompts

This document contains a collection of prompts for generating documentation for Data & Analytics code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Document ETL Pipeline Workflow](#document-etl-pipeline-workflow)
2. [Document SQL Query Logic](#document-sql-query-logic)
3. [Document API Integration](#document-api-integration)
4. [Document Business Logic Functions](#document-business-logic-functions)
5. [Document Debugging and Error Handling](#document-debugging-and-error-handling)

---

##  Document ETL Pipeline Workflow

### Purpose

To ensure clear understanding of ETL workflows for maintenance and onboarding.

### Prompt

```
Write detailed documentation for an ETL pipeline:

- Describe the extraction, transformation, and loading processes step-by-step.

- Include details about data sources, transformation rules, and target systems.

- Provide examples of input/output data and error handling mechanisms.
```

**Notes:** Keep the selection of the code while sending this prompt.

---

## Document SQL Query Logic

### Purpose

To help stakeholders understand the functionality and purpose of SQL queries.

### Prompt

```
Create documentation for complex [SQL] queries:

- Explain the purpose of the query and the business problem it solves.

- Break down the logic of joins, filters, and aggregations.

- Include sample input data and expected output for clarity.
```

**Notes:** Update SQL details.

---

## Document API Integration

### Purpose

To ensure seamless integration and troubleshooting of APIs.

### Prompt

```
Write documentation for API integration workflows:

- Describe the API endpoints used, request/response formats, and authentication methods.

- Include examples of successful and failed requests with error codes.

- Provide guidelines for handling retries, timeouts, and rate limits.
```

**Notes:** 

---

## Document Business Logic Functions

### Purpose

To clarify the functionality and usage of business-critical code.

### Prompt

```
Create documentation for business logic functions:

- Explain the purpose of each function and the calculations it performs.

- Include details about input parameters, output formats, and edge case handling.

- Provide examples of usage scenarios and expected results.
```

**Notes:** Keep the selection of the code while sending this prompt.

---

## Document Debugging and Error Handling

### Purpose

To streamline debugging and error resolution for developers and support teams.

### Prompt

```
Write documentation for debugging and error handling processes:

- Describe common errors and their root causes in your systems.

- Provide step-by-step instructions for troubleshooting and resolving issues.

- Include examples of error logs and recommended fixes.
```

**Notes:** Make sure co-pilot knows what pipelines you are referring to by selecting it in your active document within Visual Studio Code or paste the code snippet into your query.
