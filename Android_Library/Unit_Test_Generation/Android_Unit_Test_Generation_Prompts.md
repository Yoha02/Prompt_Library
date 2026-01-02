# Android Unit Test Generation Prompts

This document contains a collection of prompts for generating unit tests for Android code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Test a ViewModel's State Logic](#test-a-viewmodels-state-logic)
2. [Test a Repository's Data Caching Logic](#test-a-repositorys-data-caching-logic)
3. [Test a Jetpack Compose Component's UI and Interaction](#test-a-jetpack-compose-components-ui-and-interaction)
4. [Test a Utility or Mapper Function](#test-a-utility-or-mapper-function)

---

## Test a ViewModel's State Logic

### Purpose

Create comprehensive unit tests for a ViewModel to verify its state management logic, asynchronous operations, and interaction with its mocked dependencies.

### Prompt

```
You are an expert in Android testing using JUnit5 and MockK.

Write unit tests for my [FEATURE_NAME]ViewModel. The tests must verify its state management logic under different conditions.

- Setup:
  - Use a MainCoroutineRule to manage Dispatchers.Main for viewModelScope.
  - Mock the [REPOSITORY_NAME] dependency using mockk().

- Test Scenarios for [FUNCTION_TO_TEST]:
  - Success: When the repository returns data successfully, verify the UiState is updated with the correct data and isLoading is set to false.
  - Error: When the repository throws an exception, verify the UiState is updated with an error message and isLoading is false.
  - Loading State: Verify isLoading is true immediately after the function is called and before the repository responds.
  - Assertion: Use the Turbine library to test the sequence of StateFlow emissions (awaitItem(), awaitComplete(), etc.).

Provide the complete test class [FEATURE_NAME]ViewModelTest.kt with all necessary setup and test functions.
```

**Notes:** Testing the flow of state (Loading -> Success/Error) is a cornerstone of MVI. Turbine is the standard library for making StateFlow testing concise and reliable.

---

## Test a Repository's Data Caching Logic

### Purpose

Test the critical source-of-truth logic within a Repository, ensuring it correctly handles caching, network fetching, and data synchronization between local and remote sources.

### Prompt

```
You are an expert in testing Android data layers.

Write unit tests for my [FEATURE_NAME]Repository. The repository uses a local DAO and a remote API Service to implement a cache-first data strategy.

- Setup: Mock both the [DAO_INTERFACE] and [API_SERVICE_INTERFACE] dependencies using MockK.

- Test Scenarios for getData(forceRefresh: Boolean):
  - Cache Hit: If forceRefresh is false and the DAO has data, verify that data is returned from the DAO and the API Service is never called. (coVerify(exactly = 0) { ... })
  - Force Refresh: If forceRefresh is true, verify the API Service is called, its result is saved to the DAO, and the API data is returned.
  - Cache Miss: If forceRefresh is false and the DAO has no data, verify the API Service is called and its result is returned.

Provide the complete [FEATURE_NAME]RepositoryTest.kt test class, using runTest for all suspend test functions.
```

**Notes:** This is a vital test for any app that works offline or uses caching to reduce network usage. Verifying that the network isn't called is just as important as verifying that it is.

---

## Test a Jetpack Compose Component's UI and Interaction

### Purpose

Ensure a Composable displays data correctly and responds to user interactions as expected, preventing UI regressions in a repeatable, automated way.

### Prompt

```
You are an expert in Jetpack Compose UI testing.

Write UI tests for my [COMPONENT_NAME] Composable using the createComposeRule.

- Setup: Use composeTestRule.setContent to render the [COMPONENT_NAME] with mock data and a test onEvent lambda.

- Test Scenarios:
  - Content Verification: Use onNodeWithText and assertIsDisplayed() to verify that the Text elements correctly display the data from the provided model.
  - Interaction: Use onNodeWithTag("[TEST_TAG]") to find the clickable element, perform a performClick() action, and assert that the onEvent lambda was invoked with the correct event.
  - Existence: Verify that key nodes, like an image with a specific contentDescription, exist in the component tree.

Provide the complete UI test class for the [COMPONENT_NAME] Composable.
```

**Notes:** Use Modifier.testTag("myTestTag") on our Composables. It's the most reliable way to find specific nodes in our UI tests, especially in complex screens.

---

## Test a Utility or Mapper Function

### Purpose

Verify the correctness of pure business logic, data transformations, or utility functions. These tests are fast, stable, and form the foundation of a reliable codebase.

### Prompt

```
You are an expert in writing focused unit tests for pure Kotlin logic.

Write unit tests for my [MAPPER_OR_UTILITY_FUNCTION] using JUnit5. The tests should be small, fast, and cover all important logic paths.

- Function to Test: [FUNCTION_SIGNATURE]

- Test Scenarios:
  - Happy Path: Test the function with typical, valid input and assert the expected output.
  - Edge Cases: Test with boundary values (e.g., 0, "", empty list, null if applicable).
  - Invalid Input: If the function can receive invalid data, test that it handles it gracefully (e.g., throws an expected exception, returns a default value).

Code to Test:
kotlin
// [PASTE THE PURE KOTLIN FUNCTION or CLASS HERE]


Provide the complete, focused test class.
```

**Notes:** Mappers (e.g., DTO -> Domain Model) are perfect candidates for this type of testing. Ensuring our data transformations are correct prevents a whole class of bugs downstream.
