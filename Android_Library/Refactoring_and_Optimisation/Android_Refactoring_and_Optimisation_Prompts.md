# Android Refactoring and Optimisation Prompts

This document contains a collection of prompts for refactoring and optimizing Android code, specifically designed for use with LLM assistants like GitHub Copilot.

## Table of Contents

1. [Modernize Background Tasks](#modernize-background-tasks)
2. [Optimize a RecyclerView Adapter](#optimize-a-recyclerview-adapter)
3. [Fix Excessive Recomposition in Compose](#fix-excessive-recomposition-in-compose)
4. [Flatten a Slow XML Layout](#flatten-a-slow-xml-layout)

---

## Modernize Background Tasks

### Purpose

Update legacy, lifecycle-unaware background tasks to use modern, safer, and more efficient Kotlin Coroutines, preventing memory leaks and improving readability.

### Prompt

```
You are an expert Android developer specializing in modern concurrency.

I have a legacy Android component that uses AsyncTask to perform a background operation. Refactor this code to use Kotlin Coroutines and a ViewModel.

- Goal: Replace the AsyncTask with a call inside viewModelScope.launch.

- Architecture: The long-running work should be encapsulated in a suspend fun within a repository layer.

- State Update: The result of the operation should update a StateFlow or LiveData in the ViewModel to communicate back to the UI.

Old Code to Refactor:
kotlin
// [PASTE YOUR OLD AsyncTask or similar legacy background code HERE]


Provide the refactored ViewModel and repository function code.
```

**Notes:** Providing the exact AsyncTask code is crucial. This refactoring not only modernizes the concurrency but also improves the overall architecture by moving logic out of the UI layer (Activity/Fragment).

---

## Optimize a RecyclerView Adapter

### Purpose

Significantly improve RecyclerView performance by implementing granular list updates, which avoids re-rendering unchanged items and provides smooth animations by default.

### Prompt

```
You are an expert in Android UI performance.

My RecyclerView.Adapter is inefficient because it uses notifyDataSetChanged() for all updates. Refactor it to use the modern ListAdapter with a DiffUtil.ItemCallback.

- Data Model: The list item model is [ITEM_MODEL_CLASS].

- Task: Create a DiffUtil.ItemCallback for [ITEM_MODEL_CLASS], correctly implementing areItemsTheSame (checking unique IDs) and areContentsTheSame (checking data equality).

- Refactoring: Convert the existing adapter to extend ListAdapter and use the new DiffUtil.ItemCallback. Updates should now be handled via submitList().

Old Adapter Code:
kotlin
// [PASTE YOUR CURRENT RecyclerView.Adapter code HERE]


Provide the new DiffUtil implementation and the fully refactored ListAdapter code.
```

**Notes:** For areItemsTheSame, specify the property that serves as a unique identifier (e.g., item.id). This is the single most effective way to optimize list rendering performance.

---

## Fix Excessive Recomposition in Compose

### Purpose

Troubleshoot and fix one of the most common performance problems in Jetpack Compose, leading to a smoother, more efficient, and skippable UI.

### Prompt

```
You are an expert in Jetpack Compose performance.

My Compose screen is lagging, and the Layout Inspector shows that [COMPOSABLE_NAME] is recomposing excessively. Analyze the provided code and refactor it for optimal performance.

- Diagnose: Identify the root cause of the unnecessary recompositions (e.g., unstable parameters, creating new lambdas, reading state too deeply).

- Refactor: Apply solutions such as:
  - Ensuring data classes passed as parameters are stable (using @Stable or ImmutableList).
  - Hoisting state to a higher level.
  - Using remember for expensive calculations or lambda instances.

Problematic Composable Code:
kotlin
// [PASTE YOUR LAGGING Composable function and any relevant data classes HERE]


Provide the refactored, performance-optimized Composable code with comments explaining the changes.
```

**Notes:** Before using this prompt, it's highly recommended to use the "Recomposition Counts" feature in Android Studio's Layout Inspector to pinpoint exactly which Composable is the problem.

---

## Flatten a Slow XML Layout

### Purpose

Improve UI rendering performance and reduce layout inflation time by converting complex, nested legacy layouts into a single, efficient ConstraintLayout.

### Prompt

```
You are an expert in Android XML layout performance.

My screen is slow to load because its XML layout has deep view hierarchies with nested LinearLayout and RelativeLayout containers. Refactor this layout into a single, flat ConstraintLayout to improve performance.

- Goal: Reduce view hierarchy depth while maintaining the exact same visual appearance.

- Technique: Convert all nested layouts into a single ConstraintLayout, using chains, guidelines, and barriers where necessary to replicate the original design.

Inefficient XML Layout:
xml
<!-- [PASTE YOUR NESTED, INEFFICIENT XML LAYOUT HERE] -->


Provide the fully refactored XML layout using only one ConstraintLayout as the root.
```

**Notes:** This is especially useful for complex list items or screens that are a known performance bottleneck. ConstraintLayout is almost always the more performant choice for complex UIs.
