# React Documentation Prompts

This document contains a collection of prompts for generating React documentation, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Document React Components](#document-react-components)
2. [Document React Application](#document-react-application)
3. [Document React Hooks](#document-react-hooks)
4. [Document API Integrations](#document-api-integrations)

---

## Document React Components

### Scenario
You are developing a React application and need to create comprehensive documentation for your components. The documentation should be clear, concise, and provide examples of usage, props, and state management.

### Prompt
```
Create documentation for a React component that meets the following requirements for a [INSERT COMPONENT DETAILS HERE]:
- Provide a brief overview of the component's purpose and functionality.
- List all props with their types, default values, and descriptions.
- Include examples of how to use the component in different scenarios.
- Explain the state management approach used in the component (e.g., useState, useReducer).
- Document any side effects or lifecycle methods used.
- Include any relevant styling information (e.g., CSS modules, styled-components).
- Ensure the documentation is formatted in Markdown for easy readability.
``` 
Note: Update the component details as needed to fit your specific use case.

### Purpose
To create clear and comprehensive documentation for a React component that:
- Helps developers understand how to use the component effectively.
- Provides examples and explanations for props and state management.
- Automate the creation of code-level documentation for better maintainability.

---

## Document React Application

### Scenario
You are starting a new React application and want to create documentation that outlines the project structure, setup instructions, and key features. The documentation should be easy to follow and provide a clear overview of the application.

### Prompt
```
Create documentation for a new React application with the following features:
- Provide an overview of the application, including its purpose and key features.
- Outline the project structure, including directories for components, hooks, and utilities.
- Include setup instructions for running the application locally (e.g., dependencies, environment variables).
- Document the main App component and its role as the entry point.
- Explain the routing setup using React Router and how to navigate between pages.
- Describe the state management approach used (e.g., Context API, Redux).
- Include any styling conventions used (e.g., CSS modules, styled-components).
- Provide a README file with setup instructions and project overview.
``` 

### Purpose
To create comprehensive documentation for a React application that:
- Provides a clear overview of the project structure and setup. 
- Helps developers understand the main components and their roles.
- Documents routing and state management approaches.
---

## Document React Hooks

### Scenario
You are developing custom React hooks and need to create documentation that explains their purpose, usage, and implementation details. The documentation should be clear and provide examples for developers to follow.

### Prompt
```
Create documentation for a custom React hook that encapsulates specific logic, with the following requirements:
- Provide a brief overview of the hook's purpose and functionality.
- List all parameters and their types, along with default values and descriptions.
- Include examples of how to use the hook in different components.
- Explain the internal logic of the hook, including any state management or side effects.
- Document any dependencies or external libraries used within the hook.
- Ensure the documentation is formatted in Markdown for easy readability.
```
Note: Update the hook details as needed to fit your specific use case.  

### Purpose
To create clear and comprehensive documentation for a custom React hook that:
- Helps developers understand how to use the hook effectively.
- Provides examples and explanations for parameters and internal logic.
- Automates the creation of code-level documentation for better maintainability.
---

## Document API Integrations

### Scenario
You are integrating APIs into your React application and need to create documentation that explains how to use the APIs, including endpoints, request/response formats, and error handling. The documentation should be clear and provide examples for developers to follow.

### Prompt
```
Create documentation for API integrations in a React application with the following requirements:
- Provide an overview of the API, including its purpose and key endpoints.
- List all endpoints with their HTTP methods, request parameters, and response formats.
- Include examples of how to make API calls using fetch or axios.
- Document error handling strategies, including common error codes and how to handle them.
- Explain any authentication or authorization requirements for accessing the API.
- Include any relevant configuration details (e.g., base URL, headers).
- Ensure the documentation is formatted in Markdown for easy readability.
```
Note: Update the API details as needed to fit your specific use case.

### Purpose
To create comprehensive documentation for API integrations in a React application that:
- Provides a clear overview of the API and its endpoints.
- Helps developers understand how to make API calls and handle responses.
- Documents error handling and authentication requirements.
- Automates the creation of code-level documentation for better maintainability.
---

