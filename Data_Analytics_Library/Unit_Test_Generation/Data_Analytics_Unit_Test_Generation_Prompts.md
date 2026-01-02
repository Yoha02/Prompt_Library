# Data & Analytics Unit Test Generation Prompts

This document contains a collection of prompts for generating unit tests for Data & Analytics code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Unit Test for Data Validation Logic](#unit-test-for-data-validation-logic)
2. [Unit Test for SQL Query Results](#unit-test-for-sql-query-results)
3. [Unit Test for ETL Pipeline Components](#unit-test-for-etl-pipeline-components)
4. [Unit Test for API Integration](#unit-test-for-api-integration)
5. [Unit Test for Business Logic Functions](#unit-test-for-business-logic-functions)

---

## Unit Test for Data Validation Logic

### Purpose

To ensure the data validation logic works correctly under all conditions.

### Prompt

```
Generate unit tests to verify the accuracy of data validation logic:

- Test scenarios for null values, duplicates, and outliers.

- Include edge cases such as empty datasets or extreme values.

- Ensure the validation function flags incorrect data and passes valid data.
```

**Notes:** Keep the selection of the code while sending this prompt.
---

## Unit Test for SQL Query Results

### Purpose

To confirm the accuracy and reliability of SQL query outputs.

### Prompt

```
Write unit tests to validate the output of SQL queries:

- Test the query against mock data to ensure correct filtering, grouping, and aggregation.

- Verify that the query handles edge cases like missing values or zero records.

- Ensure the results match expected metrics for your organization's reporting needs.
```

**Notes:** Update SQL details.

---

## Unit Test for ETL Pipeline Components

### Purpose

To verify the functionality of each ETL pipeline stage independently.

### Prompt

```
Generate unit tests for individual components of the ETL pipeline:

- Test the extraction logic with mock source data.

- Validate transformation functions for correct data manipulation.

- Ensure the loading process writes data to the target system as expected.
```

**Notes:** 

---

##  Unit Test for API Integration

### Purpose

To ensure robust and reliable API integration for your organization's systems.

### Prompt

```
Write unit tests to validate API integration logic:

- Test API requests with mock responses to ensure correct handling of success and error cases.

- Verify that the integration handles timeouts, retries, and invalid responses gracefully.

- Ensure the data retrieved from the API matches expected formats and values.
```

**Notes:** Keep the selection of the code while sending this prompt.

---

##   Unit Test for Business Logic Functions

### Purpose

To validate the correctness of business logic used in analytics and reporting.

### Prompt

```
Generate unit tests for core business logic functions:

- Test calculations such as averages, percentages, and ratios with sample inputs.

- Include edge cases like division by zero or negative values.

- Ensure the functions return accurate results aligned with your organization's operational requirements.
```

**Notes:** Make sure co-pilot knows what pipelines you are referring to by selecting it in your active document within Visual Studio Code or paste the code snippet into your query.