# Android Documentation Prompts

This document contains a collection of prompts for generating documentation for Android code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Generate KDoc for a Public Class/Function](#generate-kdoc-for-a-public-classfunction)
2. [Create a Feature Module README](#create-a-feature-module-readme)
3. [Document a Custom Jetpack Compose Modifier](#document-a-custom-jetpack-compose-modifier)
4. [Document a Gradle Build Configuration](#document-a-gradle-build-configuration)

---

## Generate KDoc for a Public Class/Function

### Purpose

Automate the creation of standard, professional KDoc, making our code easier to understand, discoverable via IDE tooltips, and ready for documentation generation tools like Dokka.

### Prompt

```
You are an expert Android developer with high standards for code quality.

Generate complete KDoc documentation for the following public class and its members. The documentation must be clear, concise, and follow official Kotlin conventions.

- Class Summary: Write a brief, one-sentence summary of the class's responsibility.

- Function Docs: For each public function, provide:
  - A clear summary of what the function does.
  - A @param tag for each parameter, explaining its purpose.
  - A @return tag explaining what the function returns.

- Property Docs: Add a summary for any public properties explaining what they represent.

Code to Document:
kotlin
// [PASTE THE KOTLIN CLASS or FUNCTION YOU WANT TO DOCUMENT HERE]
```

**Notes:** This is perfect for utility classes, public API surfaces of a module, or any shared code that other developers will need to consume without reading the entire implementation.

---

## Create a Feature Module README

### Purpose

Create clear, high-level documentation that helps onboard new developers to a feature, explaining its architecture, responsibilities, and how the components work together at a glance.

### Prompt

```
You are a technical writer and Android architect.

Write a README.md file for my [FEATURE_NAME] feature module. The documentation should provide a high-level overview for any developer new to this part of the codebase.

- Title: Use a main heading for the feature name.

- Summary: Briefly explain the purpose of this feature from a user's perspective.

- Architecture:
  - State that the module follows MVVM/MVI architecture.
  - Briefly describe the responsibility of the key components: View (Compose/Fragment), ViewModel, Repository, and any major Services or Data Sources.

- Data Flow: Include a simple text-based diagram or bulleted list showing how a user action flows through the layers (e.g., View -> ViewModel -> Repository -> API -> ViewModel -> View).

- Dependencies: List any major external libraries or other internal feature modules that this module depends on.

Generate the content in Markdown format.
```

**Notes:** A good README.md in each feature module is a powerful practice in our large, modularized enterprise application. It significantly lowers the barrier to entry for developers new to our code.

---

## Document a Custom Jetpack Compose Modifier

### Purpose

Clearly document custom UI components or modifiers so that other developers on our team can easily discover, understand, and use them correctly, promoting UI consistency.

### Prompt

```
You are an expert in Jetpack Compose and technical writing.

Generate Markdown documentation for my custom Jetpack Compose Modifier. The documentation should be clear enough for any developer on my team to use it correctly.

- Purpose: A brief, clear explanation of what the modifier does and when to use it.

- Parameters: A table or bulleted list describing each parameter, its type, and its effect.

- Usage Example: A clear, copy-pasteable Kotlin code block showing how to apply the modifier to a standard Composable like Text or Box.

Custom Modifier Code:
kotlin
// [PASTE THE KOTLIN EXTENSION FUNCTION for your custom Modifier HERE]


Generate the content in Markdown format, suitable for a design system or shared UI library documentation.
```

**Notes:** As our enterprise app develops a design system, documenting custom modifiers becomes essential for maintaining a consistent look and feel across our different feature teams.

---

## Document a Gradle Build Configuration

### Purpose

Clarify complex build logic within our Gradle files, making it easier for our team to understand how to build different app variants and how environment-specific configurations are managed.

### Prompt

```
You are an expert in the Android Gradle build system.

Add comments to my build.gradle.kts file to explain a custom build configuration. The comments should clarify the purpose and usage of product flavors and build types.

- Task: For the provided Gradle snippet, add block or line comments (//) to explain:
  - The purpose of the [FLAVOR_NAME] product flavor (e.g., "for the 'pro' version of the app with extra features").
  - How a buildConfigField is defined and how it can be accessed in Kotlin code (e.g., BuildConfig.API_KEY).
  - How a resValue is defined and how it can be accessed in XML (e.g., @string/app_name).
  - The purpose of the [BUILD_TYPE_NAME] build type (e.g., "for deploying to a staging environment").

Gradle Snippet:
kotlin
// [PASTE THE productFlavors or buildTypes block from your build.gradle.kts HERE]


Provide the same Gradle snippet back, but now annotated with clear, explanatory comments.
```

**Notes:** This is invaluable in our enterprise settings where we often have multiple build variants for QA, staging, production, and different branding or feature sets.
