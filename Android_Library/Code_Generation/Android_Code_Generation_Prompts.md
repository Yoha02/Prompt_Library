# Android Code Generation Prompts

This document contains a collection of prompts for generating Android code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Generate a Standard Compose Component](#generate-a-standard-compose-component)
2. [Generate a Complete Room Entity Layer](#generate-a-complete-room-entity-layer)
3. [Generate a Hilt ViewModel with MVI-style State](#generate-a-hilt-viewmodel-with-mvi-style-state)
4. [Generate a Retrofit API Service with DTOs](#generate-a-retrofit-api-service-with-dtos)

---

## Generate a Standard Compose Component

### Purpose

Quickly scaffold a standard, reusable, and accessible Jetpack Compose UI component that follows best practices for state management and UI previews.

### Prompt

```
You are an expert Android developer specializing in Jetpack Compose.

Generate a stateless and reusable Composable function named [COMPONENT_NAME].

- State & Events: It must take a [DATA_MODEL_CLASS] for data and an onEvent: ([EVENT_CLASS]) -> Unit lambda for user actions.

- UI Structure: Use a Card as the root, with a Row containing a circular AsyncImage and a Column with two Text elements.

- Interaction: The entire Card should be clickable, triggering an [EVENT_CLASS].OnItemClicked event.

- Data Binding: Bind the AsyncImage to [IMAGE_URL_PROPERTY] and the Text elements to [TITLE_PROPERTY] and [SUBTITLE_PROPERTY].

- Styling & Accessibility: Use MaterialTheme.typography for text styles and provide a contentDescription for the image.

- Preview: Include a @Preview function with mock data to display the component in Android Studio.

Provide only the final Kotlin code.
```

**Notes:** Be specific with your class and property names (e.g., DATA_MODEL_CLASS = ArticleItem, TITLE_PROPERTY = article.headline). This prompt encourages a unidirectional data flow by using an event-based callback (onEvent).

---

## Generate a Complete Room Entity Layer

### Purpose

Efficiently create the entire persistence layer (Entity, DAO, Type Converters) for a new data model, ensuring type safety, reactivity with Flow, and proper database interaction patterns.

### Prompt

```
You are an expert Android developer specializing in data persistence with Room.

Generate a complete persistence layer for a [FEATURE_NAME] entity.

- Entity ([ENTITY_CLASS_NAME]):
  - Annotate with @Entity(tableName = "[TABLE_NAME]").
  - Define columns, including a primary key and @ColumnInfo where needed.

- DAO ([ENTITY_CLASS_NAME]Dao):
  - Include suspend functions for @Insert, @Update, and @Delete.
  - Provide reactive queries returning Flow<List<...>> for all items and Flow<...?> for a single item by ID.

- TypeConverter (Optional):
  - If the entity uses non-primitive types (e.g., Date), include a TypeConverter class to handle serialization.

Provide only the code for all required classes.
```

**Notes:** This prompt intentionally omits the @Database class, as in our enterprise app, we would add the new entity and DAO to our existing AppDatabase class, not create a new one.

---

## Generate a Hilt ViewModel with MVI-style State

### Purpose

Scaffold a robust, testable ViewModel that adheres to modern MVI principles (single state, events), integrates with Hilt for dependency injection, and manages its state lifecycle correctly.

### Prompt

```
You are an expert Android developer using modern MVI (Model-View-Intent) architecture.

Generate a [FEATURE_NAME]ViewModel using Hilt.

- State & Events:
  - Define a single [FEATURE_NAME]UiState data class for all screen state.
  - Define a [FEATURE_NAME]Event sealed interface for all user actions.

- Dependency Injection: Use @HiltViewModel and inject dependencies like [REPOSITORY_NAME] via the constructor.

- State Management:
  - Expose a single, read-only StateFlow<[FEATURE_NAME]UiState> to the UI.
  - Implement a public onEvent function to process UI events and trigger logic within viewModelScope.

Provide only the code for the ViewModel, UiState, and Event classes.
```

**Notes:** This pattern strongly encourages separating "what happened" (Events) from "how to handle it" (ViewModel logic), leading to cleaner, more predictable code in large applications.

---

## Generate a Retrofit API Service with DTOs

### Purpose

Quickly define a type-safe network layer for a feature, including request/response models (DTOs) that are separate from the app's domain models, and demonstrate common API interaction patterns like auth headers.

### Prompt

```
You are an expert in Android networking.

Generate the API contract for a [FEATURE_NAME] feature using Retrofit.

- Interface ([API_NAME]ApiService):
  - Define suspend functions for GET, POST, and PUT operations.
  - Use @Path, @Query, @Body, and @Header annotations correctly for parameters and authorization.

- DTOs (Data Transfer Objects):
  - For each request and response, define a corresponding Kotlin data class.
  - Use serialization annotations (e.g., @SerializedName) to map JSON keys to Kotlin properties.

Provide only the code for the Retrofit interface and all DTO classes.
```

**Notes:** Keeping DTOs separate from domain models is a key architectural principle. This allows the API contract to change without forcing changes throughout our entire app's domain logic.
