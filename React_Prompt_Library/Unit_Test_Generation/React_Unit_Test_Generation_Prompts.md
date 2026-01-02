# React Unit Test Generation Prompts

This document contains a collection of prompts for generating unit tests for React applications, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Generate Unit Tests for React Components](#generate-unit-tests-for-react-components)
2. [Generate Unit Tests for React Hooks](#generate-unit-tests-for-react-hooks)
3. [Generate Unit Tests for React Context](#generate-unit-tests-for-react-context)
4. [Generate Unit Tests for API Integrations](#generate-unit-tests-for-api-integrations)

---

## Generate Unit Tests for React Components

### Scenario
You have developed a React component and need to create unit tests to ensure its functionality. The tests should cover various scenarios, including rendering, props validation, and interaction handling. The goal is to ensure the component behaves as expected and is resilient to changes.

### Prompt
```
Create unit tests for a React component that meets the following requirements for a [INSERT COMPONENT DETAILS HERE]:
- Use Jest and React Testing Library for testing.
- Test the component's rendering with different props.
- Validate that the component handles props correctly (e.g., default values, required props).
- Include tests for user interactions (e.g., button clicks, form submissions).
- Ensure that the component's state updates correctly based on user interactions.
- Test edge cases, such as invalid props or unexpected user input.
- Include snapshots for visual regression testing.
- Ensure the tests are well-structured and easy to read.
```
Note: Update the component details as needed to fit your specific use case. 

### Purpose
To create comprehensive unit tests for a React component that:
- Ensures the component behaves correctly under various conditions.
- Validates props handling and user interactions.
- Provides a safety net for future changes, helping to catch regressions early.

---

## Generate Unit Tests for React Hooks

### Scenario
You have developed a custom React hook and need to create unit tests to verify its functionality. The tests should cover different scenarios, including state management, side effects, and error handling. The goal is to ensure the hook works as intended and is robust against changes.

### Prompt
```
Create unit tests for a custom React hook that meets the following requirements for a [INSERT HOOK DETAILS HERE]:
- Use Jest and React Testing Library for testing.
- Test the hook's initial state and default values.
- Validate that the hook updates state correctly based on user interactions or external changes.
- Include tests for side effects (e.g., API calls, timers) and ensure they are handled correctly.
- Test error handling scenarios, such as invalid inputs or failed API calls.
- Ensure that the hook can be used in a component and behaves as expected when integrated.
- Include any necessary mocks for dependencies (e.g., API calls, context).
- Ensure the tests are well-structured and easy to read.
```
Note: Update the hook details as needed to fit your specific use case.      

### Purpose
To create comprehensive unit tests for a custom React hook that:
- Ensures the hook behaves correctly under various conditions.
- Validates state management and side effects.
- Provides a safety net for future changes, helping to catch regressions early.

---

## Generate Unit Tests for React Context

### Scenario
You have developed a React Context to manage global state and need to create unit tests to verify its functionality. The tests should cover different scenarios, including context value updates, consumer behavior, and error handling. The goal is to ensure the context works as intended and is resilient to changes.   

### Prompt
```
Create unit tests for a React Context that meets the following requirements for a [INSERT CONTEXT DETAILS HERE]:
- Use Jest and React Testing Library for testing.
- Test the context provider's initial value and default state.
- Validate that the context value updates correctly when actions are dispatched.
- Include tests for consumer components to ensure they receive the correct context value.
- Test edge cases, such as invalid actions or unexpected context values.
- Ensure that the context can be used in a component and behaves as expected when integrated.
- Include any necessary mocks for dependencies (e.g., API calls, other contexts).   
- Ensure the tests are well-structured and easy to read.
```
Note: Update the context details as needed to fit your specific use case.


### Purpose
To create comprehensive unit tests for a React Context that:
- Ensures the context behaves correctly under various conditions.
- Validates context value updates and consumer behavior.
- Provides a safety net for future changes, helping to catch regressions early.

---

## Generate Unit Tests for API Integrations

### Scenario
You have integrated an external API into your React application and need to create unit tests to verify the integration. The tests should cover different scenarios, including successful API calls, error handling, and data transformations. The goal is to ensure the API integration works as intended and is resilient to changes.

### Prompt
```
Create unit tests for an API integration in a React application that meets the following requirements for a [INSERT API DETAILS HERE]:
- Use Jest and React Testing Library for testing.
- Test successful API calls and ensure the data is correctly fetched and displayed.
- Validate error handling scenarios, such as network failures or API errors.
- Include tests for loading states and how the application behaves during API calls.
- Ensure that the API integration can be used in a component and behaves as expected when integrated.
- Include any necessary mocks for the API calls (e.g., using jest.mock or msw).
- Ensure the tests are well-structured and easy to read.
``` 
Note: Update the API details as needed to fit your specific use case.

### Purpose
To create comprehensive unit tests for an API integration in a React application that:
- Ensures the API integration behaves correctly under various conditions.
- Validates successful API calls and error handling.
- Provides a safety net for future changes, helping to catch regressions early.

---
