# Data & Analytics Code Generation Prompts

This document contains a collection of prompts for generating Data & Analytics code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Data Extraction](#data-extraction)
2. [Data Transformation](#data-Transformation)
3. [Data Validation](#data-validation)
4. [Data Aggregation](#data-aggregation)
5. [Trend Analysis](#trend-analysis)
6. [Anomaly Detection](#anomaly-detection)
7. [Predictive Analytics](#predictive-analytics)
8. [Data Visualization](#data-visualization)
9. [Performance Optimization](#performance-optimization)
10. [ETL Pipeline](#etl-pipeline)

---

## Data Extraction

### Purpose

To retrieve raw data from your organization's systems for analytics, reporting, and operational monitoring.

### Prompt

```

Write [LANGUAGE] code to extract data from [YOUR OPERATIONAL SYSTEMS OR DATABASES OR APIs]:

- Include logic to handle large datasets efficiently.

- Ensure incremental data extraction for scalability.

- Incorporate error handling for missing or corrupted data.

```

**Notes:** Be specific about the what language you want to use, from what system you want to extract the data, replace [VARIABLE] with the actual required input.

---

## Data Transformation

### Purpose

To clean and structure data for operational reporting and decision-making.

### Prompt

```

Generate code to transform raw data into actionable insights for [TABLE NAME / PARTICULAR DATA]:

- Apply filtering, sorting, and grouping operations based on [BUSINESS REQUIREMENTS].

- Perform calculations such as averages, percentages, and ratios.

- Ensure the code is modular and reusable for future transformations.

```

**Notes:** Update table details and business context in this prompt.

---

## Data Validation

### Purpose

To ensure the accuracy and reliability of data before it is used for analytics or alerts.

### Prompt

```

Write code to validate the quality of data in [TABLE / GROUP OF TABLES]:

- Check for null values, duplicates, and outliers.

- Flag records that fail validation and log them for review.

- Provide a summary of validation results for further investigation.

```

**Notes:** Add context of what table or group of table the data validation has to happen. Also, make sure the sample data or structure of the table is selected when sending this prompt to LLM.

---

## Data Aggregation

### Purpose

To summarize data into meaningful metrics for dashboards, reports, or decision-making.

### Prompt

```

Generate code to aggregate data for [SYSTEM / BUSINESS FUNCTION] reporting needs:

- Group data by dimensions such as store, region, or product category.

- Calculate metrics like sum, average, count, and percentage.

- Ensure the code handles edge cases like missing or zero values.

```

**Notes:** Please update the system or function's name for which reporting needs are there.

---

## Trend Analysis

### Purpose

To identify patterns and changes in data over time for forecasting and strategic planning.

### Prompt

```

Write code to analyze trends in [TABLE / BUSINESS FUNCTION] data over time:

- Group data by time intervals (e.g., daily, weekly, monthly).

- Calculate growth rates, moving averages, or seasonality patterns.

- Visualize trends using charts or graphs for operational dashboards.

```

**Notes:** This prompt should return boilerplate code for doing trend analysis which can be personalized by providing additional context.

---

## Anomaly Detection

### Purpose

To identify unusual data points that may indicate errors, fraud, or operational inefficiencies.

### Prompt

```

Generate code to detect anomalies in [TABLE / BUSINESS FUNCTION] data:

- Identify outliers based on statistical methods (e.g., z-score, IQR).

- Flag records that deviate significantly from expected patterns.

- Provide a summary of anomalies for further investigation.

```

**Notes:** Add the context of table or the data from which anomaly detection code is needed.

---

## Predictive Analytics

### Purpose

To leverage historical data and statistical models to predict future outcomes and trends.

### Prompt

```

Write code to implement predictive analytics for [TABLE / BUSINESS FUNCTION]:

- Use historical data to forecast future values (e.g., sales, demand, delays).

- Apply machine learning models (e.g., regression, classification).

- Ensure the code is scalable and supports real-time predictions.

```

**Notes:** Add the context of table or the data from which predictive analytics code is needed.

---

## Data Visualization

### Purpose

To present data insights in an intuitive and visually appealing way for stakeholders.

### Prompt

```

Generate code to visualize data insights for [DOMAIN NAME / TABLE NAME for example, Supply Chain PowerBI Cockpit, OMNI Dashboards, etc.] dashboards:

- Create charts (e.g., bar, line, pie) to summarize key metrics.

- Include interactivity for filtering and drilling down into data.

- Ensure the visualizations are optimized for operational dashboards.

```

**Notes:** Please keep the selection of the sample data or table schema if more relevant code generation is needed.

---

## Performance Optimization

### Purpose

To improve the efficiency and scalability of data processing for large datasets or complex queries.

### Prompt

```

Write code to optimize data processing workflows (can be a DAG or its SQL, ETL code) for [SYSTEM / JOB NAME]:

- Use indexing, partitioning, or caching to improve query performance.

- Minimize memory usage for large datasets.

- Provide recommendations for scaling the solution across your organization's systems.

```

**Notes:** Provide DAG or its SQL as an input while sending the prompt to LLM for better results. 

---

## ETL Pipeline

### Purpose

To automate the process of extracting, transforming, and loading data into a target system for analytics or reporting.

### Prompt

```

Generate [LANGUAGE or FRAMEWORK for example JAVA Spring Batch, Airflow DAG] code for an ETL pipeline tailored to your organization's operations:

- Extract data from multiple sources such as databases and APIs.

- Transform data to meet business requirements.

- Load data into a target system (e.g., data warehouse, reporting database).

- Ensure the pipeline is robust, automated, and handles errors gracefully.

```

**Notes:** The Language and framework selection will depend on the team and the domain's preference. 