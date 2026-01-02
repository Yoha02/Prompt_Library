# Data & Analytics Refactoring and Optimisation Prompts

This document contains a collection of prompts for refactoring and optimizing Data & Analytics code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Code Refactoring for Maintainability](#code-refactoring-for-maintainability)
2. [Query Optimization for Performance](#query-optimization-for-performance)
3. [Algorithm Optimization](#algorithm-optimization)
4. [Code Cleanup for Legacy Systems](#code-cleanup-for-legacy-systems)
5. [Resource Optimization in ETL Pipelines](#resource-optimization-in-etl-pipelines)

---

## Code Refactoring for Maintainability

### Purpose

To make the codebase easier to understand, maintain, and extend.

### Prompt

```
Refactor existing code to improve readability and maintainability:

- Break down large functions or queries into smaller, reusable components.

- Use consistent naming conventions aligned with your organization's standards.

- Remove redundant logic and ensure the code is modular for future updates.
```

**Notes:** Keep the selection of the code while sending this prompt.

---

## Query Optimization for Performance

### Purpose

To enhance the performance of data retrieval and processing in operational systems.

### Prompt

```
Optimize [SQL] to improve execution time and resource usage:

- Identify and eliminate unnecessary joins or subqueries.

- Implement indexing and partitioning strategies for large tables.

- Ensure the query scales efficiently for your organization's high-volume datasets.
```

**Notes:** Update SQL details.

---

## Algorithm Optimization

### Purpose

To improve the speed and scalability of algorithms used in your organization's workflows.

### Prompt

```
Refactor algorithms to improve efficiency and reduce computational complexity:

- Replace nested loops or inefficient logic with optimized approaches.

- Use caching or memoization to avoid redundant calculations.

- Ensure the algorithm handles edge cases and scales for large datasets.
```

**Notes:** Post optimization, please perform sanity check to make sure any core logic is not changed. 

---

##  Code Cleanup for Legacy Systems

### Purpose

Improve UI rendering performance and reduce layout inflation time by converting complex, nested legacy layouts into a single, efficient ConstraintLayout.

### Prompt

```
Refactor legacy code to align with modern best practices:

- Replace outdated syntax or deprecated functions with current standards.

- Remove hardcoded values and replace them with configurable parameters.

- Ensure the refactored code integrates seamlessly with your organization's existing systems.
```

**Notes:** This is especially useful for complex list items or screens that are a known performance bottleneck. ConstraintLayout is almost always the more performant choice for complex UIs.

---

##  Resource Optimization in ETL Pipelines

### Purpose

To streamline ETL processes for faster and more efficient data handling.

### Prompt

```
Optimize ETL pipelines to reduce resource consumption and improve throughput:

- Implement parallel processing or batch operations for large datasets.

- Minimize memory usage by streaming data instead of loading it entirely into memory.

- Ensure error handling and logging are efficient and do not impact performance.
```

**Notes:** Make sure co-pilot knows what pipelines you are referring to by selecting it in your active document within Visual Studio Code or paste the code snippet into your query.
