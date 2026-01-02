# React Code Generation Prompts

This document contains a collection of prompts for generating React code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Implement React Components](#implement-react-components)
2. [Build React Application](#build-react-application)
3. [Create React Hooks](#create-react-hooks)
4. [Integrate with APIs](#integrate-with-apis)
5. [Create Zustand Store](#create-zustand-store)


---

## Implement React Components

### Scenario
You are developing a React application and need to create reusable components that follow best practices for maintainability and performance. The components should be modular, well-documented, and easy to test.

### Prompt
```
Create a React component that meets the following requirements for a [INSERT COMPONENT DETAILS HERE]:
- The component should be a functional component using React hooks.
- It should accept props for customization (e.g., title, content).
- Implement basic state management using the useState hook.
- Include PropTypes for type checking.
- Ensure the component is styled using CSS modules or styled-components.
- Add unit tests using Jest and React Testing Library.
- Include comments explaining the purpose of each part of the code.
- Ensure the component is reusable and can be easily integrated into other parts of the application.
``` 


### Purpose
To build a reusable, well-structured React component that:
- Demonstrates best practices in React development.
- Uses hooks for state management.
- Is type-safe with PropTypes.
- Is styled appropriately and tested thoroughly.   

---

## Build React Application

### Scenario
You are starting a new React application and want to set up a clean, maintainable project structure that follows best practices. The application should be modular, easy to navigate, and ready for future enhancements.

### Prompt
```
Create a new React application with the following features: [INSERT APPLICATION DETAILS HERE]
- Use Create React App or Vite for setup.
- Organize the project structure into components, hooks, and utilities directories.
- Include a main App component that serves as the entry point.
- Implement routing using React Router.
- Set up state management using Context API or Redux.
- Include a basic layout with a header, footer, and main content area.
- Ensure the application is responsive and accessible.
- Add basic styling using CSS modules or styled-components.
- Include a README file with setup instructions and project overview.
```
Note: Update the application details as needed to fit your specific use case.

### Purpose
To create a well-structured React application that:
- Follows best practices for project organization.
- Implements routing and state management.
- Is responsive and accessible.
- Provides a solid foundation for future development.

---

## Create React Hooks

### Scenario
You need to create custom React hooks to encapsulate specific logic that can be reused across different components. The hooks should be modular, well-documented, and easy to test.

### Prompt
```
Create a custom React hook that implements the following functionality: [INSERT FUNCTIONALITY HERE]
The hook should:
- Be a functional component using React hooks.
- Accept parameters for customization (e.g., initial state, options).
- Use useState and useEffect hooks for state management and side effects.
- Include error handling and validation.
- Be reusable across different components.
- Include comments explaining the purpose of each part of the code.
- Include unit tests using Jest and React Testing Library.
```
Note: Replace `[INSERT FUNCTIONALITY HERE]` with the specific functionality you want to implement.

### Purpose
To create a custom React hook that:
- Encapsulates specific logic for reuse.
- Is modular and easy to integrate into components.
- Is well-documented and tested.

---

## Integrate with APIs

### Scenario
You need to integrate a React application with an external API to fetch and display data. The integration should be efficient, handle errors gracefully, and provide a good user experience.

### Prompt
```
Integrate the following API into a React application: [INSERT API DETAILS HERE]
The integration should:
- Create a service module to handle API requests.
- Use Axios or Fetch API for making requests.
- Implement error handling for API calls.
- Use React hooks to manage API state (loading, error, data).
- Display the fetched data in a component.
- Ensure the component is responsive and user-friendly.
- Include comments explaining the purpose of each part of the code.
- Include unit tests for the API service and component using Jest and React Testing Library.
```
Note: Replace `[INSERT API DETAILS HERE]` with the specific API details you want to integrate

### Purpose
To integrate a React application with an external API that:
- Fetches and displays data efficiently.
- Handles errors gracefully.
- Provides a good user experience.

---

## Create Zustand Store

### Scenario
You need to create a Zustand store for state management in a React application. The store should be modular, easy to use, and follow best practices for state management.

### Prompt
```
Create a Zustand store for managing state in a React application with the following requirements: [INSERT STORE DETAILS HERE]
- The store should manage global state (e.g., user authentication, application settings).
- Use Zustand for state management.
- Implement actions for updating state (e.g., login, logout, update settings).
- Ensure the store is modular and can be easily integrated into components.
- Include comments explaining the purpose of each part of the code.
- Include unit tests for the store using Jest.
- Ensure the store is easy to use in functional components with hooks.
```
Note: Replace `[INSERT STORE DETAILS HERE]` with the specific state management requirements you want to implement.

### Purpose
To create a Zustand store that:
- Manages global state in a React application.
- Is modular and easy to integrate into components.
- Follows best practices for state management.
- Is well-documented and tested.

---
