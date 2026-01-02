# Backend API Debugging and Explanation Prompts

This document contains a collection of prompts for debugging and explaining BackendAPI code, specifically designed for use with LLM assistants like GitHub Copilot.


##  Provide a checklist for troubleshooting common API errors.

### Scenario

Suggest debugging steps for the different  application errors .  Ex: 500/ XXX Internal Server Error.

### Prompt

```
// Backend [Specify Language/Framework and Validation Library, e.g., Python FastAPI with Pydantic / Java with SpringBoot etc]: 

// API Debugging: My API endpoint is returning a 500 Internal Server Error. What are the common causes and what steps should I take to debug this in a [Specify Language/Framework, e.g., Node.js Express] application? (e.g., check logs, use debugger, simplify code).  . .Error Details:   [ Error details form stacktrace/grafana logs etc]

Include:
1. Common causes of 500 errors in backend APIs.
2. Step-by-step debugging checklist:
   - Log inspection
   - Stack trace analysis

Optional: How to reproduce the issue locally or in a staging environment.

```
