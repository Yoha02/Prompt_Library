# iOS Refactoring and Optimisation Prompts

This document contains prompts for refactoring and optimizing iOS code using the VIPER architecture pattern.

## Table of Contents

1. [Separate Concerns & Simplify Logic](#separate-concerns--simplify-logic)
2. [Optimize Performance or Memory](#optimize-performance-or-memory)
3. [Protocol & Dependency Injection Refactor](#protocol--dependency-injection-refactor)
4. [Code Cleanup and Readability](#code-cleanup-and-readability)
5. [Consolidate Feature Module](#consolidate-feature-module)

---

## Separate Concerns & Simplify Logic

### Use Case
Use this prompt when a VIPER component (Interactor or Presenter) has grown too complex or is doing more than one job. It helps refactor the code to better adhere to single-responsibility principles. For example, if a Presenter is directly performing data parsing or a view controller has business logic, this prompt guides splitting that into the proper layer or a new helper class. The goal is to reduce coupling and make each component focus on its defined role for maintainability.

### Scenario
Refactoring overly complex components to improve separation of concerns.

### Prompt
Refactor the [FeatureName]Presenter/Interactor to improve separation of concerns. Identify any logic in [Presenter/Interactor] that does not belong to its core responsibility (e.g. formatting details in Interactor or network calls in Presenter) and move it to the appropriate layer (Presenter, Interactor, or a new helper/manager class). Ensure each class has a single reason to change. After refactoring, the components should communicate via protocols as in VIPER, reducing tight coupling. Provide the refactored code with brief comments explaining how this change makes the code cleaner and more maintainable.

### Example

**Problem**: RewardsDashboardPresenter that formats points and updates badge UI directly.

**Before**:
```swift
let formattedPoints = "\(reward.points) points"
badgeView.updateText(formattedPoints)
```

**After**:
```swift
// Move formatting to RewardFormatter
let formattedPoints = rewardFormatter.formatPoints(reward.points)
view?.updateBadgeText(formattedPoints)
```

**Benefits**: 
- Formatting logic is reusable
- Presenter focuses on coordination
- Easier to unit test formatting separately

---

## Optimize Performance or Memory

### Use Case
Use this prompt when you need to improve the performance of a component or address memory issues. For example, an Interactor method that processes a large list could be optimized, or a retain cycle between Presenter and View might need fixing. The prompt encourages profiling and using Swift best practices for optimization without breaking VIPER architecture.

### Scenario
Improving performance bottlenecks or resolving memory issues in VIPER components.

### Prompt
Optimize the [FeatureName] module's implementation for [performance/memory]. For instance, if [FeatureName]Interactor has a slow loop or an expensive operation, refactor it using more efficient algorithms or async processing (e.g. use GCD or async/await to offload to background thread). If there are memory leaks (e.g. a strong reference cycle between Presenter and View), adjust the code (use weak references or other techniques) to resolve them. Ensure that the refactored code remains correct and that all VIPER layers interact properly. Provide before-and-after pseudo-code or explanations for clarity, and make sure all optimizations follow Swift best practices (no premature optimization that sacrifices clarity).

### Example

**Problem**: RewardsDashboardInteractor processing 1000 rewards synchronously.

**Before**:
```swift
for reward in rewards {
    process(reward)
}
```

**After (Async)**:
```swift
DispatchQueue.global(qos: .userInitiated).async {
    let processed = rewards.map { self.process($0) }
    DispatchQueue.main.async {
        self.presenter?.didProcessRewards(processed)
    }
}
```

**Benefits**:
- Non-blocking UI
- Better user experience
- Proper threading separation

---

## Protocol & Dependency Injection Refactor

### Use Case
Use this prompt to improve testability and modularity by decoupling components. If, for example, the Interactor is directly instantiating a service or the Presenter is tightly coupled to a concrete view class, this refactoring prompt introduces protocols and dependency injection. This reduces dependencies, making it easier to swap implementations (e.g. use mocks) and adhere to VIPER's modular structure.

### Scenario
Reducing tight coupling between components through protocols and dependency injection.

### Prompt
Refactor [FeatureName] module to decouple dependencies using protocols and dependency injection. Specifically, identify any places where the code directly uses concrete classes from another layer (e.g. Interactor directly creating a network request or Presenter assuming a concrete UIViewController). Define protocols for these interactions (e.g. a RemoteServiceProtocol or ViewInterface protocol) and have the Interactor/Presenter depend on those instead of concrete types. Inject these dependencies via initializer or property, so that in tests a mock implementation can be provided. Show the updated class definitions and initializations, ensuring the module remains functionally the same but with reduced coupling and improved testability.

### Example

**Problem**: Direct dependency on concrete service class.

**Before**:
```swift
let service = RewardsRemoteService()
```

**After**:
```swift
init(service: RewardsServiceProtocol) {
    self.service = service
}
```

**Benefits**:
- Testable with mock services
- Flexible implementation swapping
- Reduced coupling

---

## Code Cleanup and Readability

### Use Case
Use this prompt when code works but is hard to read or maintain. It focuses on refactoring for clarity: breaking down long functions, renaming variables for clarity, removing duplicate code, and improving structure. This is applicable across any VIPER component; for instance, if an Interactor function is 200 lines long, or similar code exists in two Presenters, this prompt guides cleaning it up.

### Scenario
Improving code readability and maintainability without changing functionality.

### Prompt
Clean up and refactor the [FeatureName] code to improve readability and maintainability. For example, if [FeatureName]Interactor has a very long function or repeated logic, split it into smaller private functions with descriptive names. Remove any duplicate code by abstracting common functionality (possibly into a shared utility or extension if appropriate). Ensure that the refactored code follows Swift naming conventions and is well-commented where complex. No functionality should change – only the internal structure – and all VIPER layer boundaries (the protocols and data flow) should remain consistent. Provide a summary of changes made for clarity.

### Example

**Problem**: Long, complex reward points handling function.

**Before**:
```swift
func handleRewardPoints() {
    if points > 0 {
        // complex logic here
    } else {
        // different complex logic here
    }
}
```

**After**:
```swift
func handleRewardPoints() {
    points > 0 ? processEarnedPoints() : handleZeroPoints()
}

private func processEarnedPoints() {
    // extracted earned points logic
}

private func handleZeroPoints() {
    // extracted zero points logic
}
```

**Benefits**:
- Smaller, focused functions
- Self-documenting code
- Easier to test individual behaviors

---

## Consolidate Feature Module

### Use Case
Use this when a feature's code is scattered or not consistently structured. In large teams, different developers might create slightly divergent patterns; this prompt helps unify the structure. For example, if the Order Management feature has multiple sub-modules or duplicate models, refactor to consolidate models and ensure a single source of truth, or merge small VIPER modules if they belong together. This keeps the project scalable and easier to navigate.

### Scenario
Reorganizing and consolidating scattered feature code for better structure.

### Prompt
Restructure the [FeatureName] module for consistency and scalability. Look for any redundant classes or structs (for instance, multiple data models representing the same concept, or separate VIPER modules that could be combined). Refactor by consolidating duplicate models into one Entity or merging closely related functionality into a single module if it simplifies the architecture. Update the folder structure if needed so that all [FeatureName] components (Interactor, Presenter, View, etc.) are in the right place. Ensure that after refactoring, all references are updated and the feature's functionality is unchanged, but the code organization is cleaner and more feature-centric. Provide an outline of the new structure and justify how it improves the codebase.

### Example

**Problem**: Multiple similar reward models scattered across the codebase.

**Before**:
- `RewardViewModel`
- `RewardItemModel` 
- `RewardDataModel`

**After**:
```swift
struct RewardModel {
    let id: String
    let title: String
    let points: Int
}
```

**Benefits**:
- Single source of truth
- Reduced confusion
- Easier maintenance

---

## Best Practices for Refactoring

### General Guidelines
- **Incremental Changes**: Make small, testable changes
- **Preserve Functionality**: Ensure behavior remains the same
- **Maintain VIPER Boundaries**: Keep layer responsibilities clear
- **Test Coverage**: Verify tests still pass after refactoring
- **Documentation**: Update comments and documentation as needed

### Performance Optimization Tips
- **Profile First**: Use Instruments to identify actual bottlenecks
- **Async Operations**: Move heavy work off the main thread
- **Memory Management**: Use weak references appropriately
- **Lazy Loading**: Load data only when needed

### Code Quality Improvements
- **Naming Conventions**: Use descriptive, self-documenting names
- **Function Size**: Keep functions small and focused
- **DRY Principle**: Don't repeat yourself
- **SOLID Principles**: Follow object-oriented design principles 