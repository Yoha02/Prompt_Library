# iOS Documentation Prompts

This document contains prompts for creating comprehensive documentation for iOS applications using the VIPER architecture pattern.

## Table of Contents

1. [Interactor API Documentation](#interactor-api-documentation)
2. [Presenter API Documentation](#presenter-api-documentation)
3. [Entity Model Documentation](#entity-model-documentation)
4. [Module Overview and Usage](#module-overview-and-usage)
5. [API Endpoint Documentation in Remote Service](#api-endpoint-documentation-in-remote-service)

---

## Interactor API Documentation

### Use Case
Use this prompt when you want to add or update the documentation for an Interactor's public interface. It ensures that all public methods and the purpose of the Interactor are clearly described using Swift's triple-slash comments (`///`). This helps other developers quickly understand the business logic provided by the Interactor and how to use it.

### Scenario
Documenting Interactor business logic methods and their responsibilities.

### Prompt
Add Swift documentation comments to the **[FeatureName]Interactor** and its protocols. Document the purpose of the Interactor (e.g. "/// Interactor for [FeatureName], handles business logic for the feature"). Then for each function in the **InteractorInput** protocol, write a `///` comment describing the function's intent, parameters, and what outcome it triggers. Also document any **InteractorOutput** protocol methods that the Interactor calls on the Presenter. This ensures all team members know how the Interactor handles business logic and communicates with other VIPER components.

### Example

```swift
/// Interactor for managing reward data and business logic
/// Handles fetching, processing, and validating reward information
protocol RewardsDashboardBusinessLogic {
    /// Fetches all available rewards from the remote service
    /// Triggers presenter update with results or error
    func fetchRewards()
    
    /// Validates if user can claim a specific reward
    /// - Parameter rewardId: The unique identifier of the reward
    /// - Parameter userPoints: Current user's point balance
    func validateRewardClaim(rewardId: String, userPoints: Int)
}

/// Output protocol for communicating results back to presenter
protocol RewardsDashboardPresentationLogic {
    /// Called when rewards are successfully fetched
    /// - Parameter rewards: Array of available reward items
    func presentRewards(_ rewards: [Reward])
    
    /// Called when an error occurs during reward operations
    /// - Parameter message: User-friendly error message
    func presentError(_ message: String)
}
```

---

## Presenter API Documentation

### Use Case
Use this prompt for writing documentation comments on Presenter methods and any Presenter-to-View or Presenter-to-Interactor protocol definitions. Since the Presenter orchestrates the flow, documenting its interface is vital. This prompt makes sure anyone reading the code understands the presenter's responsibilities and how to interact with it.

### Scenario
Documenting presentation logic and view communication interfaces.

### Prompt
Add Swift documentation comments to the **[FeatureName]Presenter** and its related protocols. Document the purpose of the Presenter (e.g. "/// Presenter for [FeatureName], handles presentation logic and user input for the feature"). Then for each function in the **ViewToPresenter** protocol, write a `///` comment describing the function's intent, parameters, and what outcome it triggers. Also document the **PresenterToView** protocol methods that the Presenter calls on the View. This ensures all team members know how the Presenter mediates between View and Interactor.

### Example

```swift
/// Presenter handles formatting and user interaction for Rewards Dashboard
/// Mediates between View layer and business logic, transforming data for display
protocol RewardsDashboardViewToPresenter {
    /// Called when the view finishes loading
    /// Triggers initial data fetch from interactor
    func viewDidLoad()
    
    /// Called when user selects a reward item
    /// - Parameter rewardId: The selected reward's unique identifier
    func didSelectReward(rewardId: String)
    
    /// Called when user taps the refresh button
    /// Initiates fresh data fetch from remote service
    func didTapRefresh()
}

/// Protocol for presenter to communicate with view
protocol RewardsDashboardPresenterToView: AnyObject {
    /// Updates view with formatted reward display data
    /// - Parameter viewModels: Array of formatted reward view models
    func displayRewards(_ viewModels: [RewardViewModel])
    
    /// Shows error message to user
    /// - Parameter message: Localized error message
    func displayError(_ message: String)
    
    /// Shows/hides loading indicator
    /// - Parameter isLoading: Whether to show loading state
    func setLoading(_ isLoading: Bool)
}
```

---

## Entity Model Documentation

### Use Case
Use this prompt to document the data models (Entities) used in a feature. Public structs or classes that represent data should have documentation on their purpose and any non-obvious behavior. This is especially helpful in modular environments where models might be shared across modules.

### Scenario
Documenting data models and their properties for clarity and reusability.

### Prompt
Write documentation comments for the **[EntityName]** model in **[FeatureName]**. Begin with a brief description of what the entity represents. Document any important properties, especially if their purpose might not be obvious from the name. If the entity has custom initializers or methods, document those as well. Use proper formatting for parameters and return values in method docs. The goal is to make sure anyone reading the codebase can understand the role and usage of this data model at a glance.

### Example

```swift
/// Model representing a reward item in the loyalty program
/// Contains all information needed to display and process reward claims
struct Reward: Codable {
    /// Unique identifier for the reward
    let id: String
    
    /// Display title shown to users
    let title: String
    
    /// Number of points required to claim this reward
    let points: Int
    
    /// Detailed description of the reward benefit
    let description: String
    
    /// Indicates if this is a premium tier reward (requires 500+ points)
    var isPremium: Bool {
        return points >= 500
    }
    
    /// Formatted display text combining title and points
    /// - Returns: String in format "Title (XXX pts)"
    var displayText: String {
        return "\(title) (\(points) pts)"
    }
    
    /// Validates if the reward data is complete and valid
    /// - Returns: true if all required fields are present and valid
    var isValid: Bool {
        return !id.isEmpty && !title.isEmpty && points > 0
    }
}
```

---

## Module Overview and Usage

### Use Case
Use this prompt to create higher-level documentation for the entire module or a complex workflow. This provides context on how the module's pieces work together, which is valuable for onboarding new team members.

### Scenario
Creating comprehensive module documentation for understanding overall architecture.

### Prompt
Create an overview documentation for the **[FeatureName]** module. This should outline how the VIPER components interact for this feature. Explain the flow starting from the View (user actions) to Presenter to Interactor to RemoteService, and back to Presenter and View. Mention key classes and protocols by name to make it clear. By the end of this documentation, a developer should understand the responsibilities of each part of **[FeatureName]** and how to extend or use this module.

### Example

```markdown
# RewardsDashboard Module

## Overview
The RewardsDashboard module implements a complete VIPER architecture for displaying and managing user rewards in the loyalty program.

## Component Responsibilities

### View (`RewardsDashboardViewController`)
- Displays rewards list in table view
- Handles user interactions (tap, refresh, claim)
- Shows loading states and error messages
- Implements `RewardsDashboardPresenterToView` protocol

### Presenter (`RewardsDashboardPresenter`)
- Mediates between View and Interactor
- Formats raw data into view models
- Handles user input validation
- Implements `RewardsDashboardViewToPresenter` and `RewardsDashboardPresentationLogic`

### Interactor (`RewardsDashboardInteractor`)
- Contains core business logic for rewards
- Validates reward claims against user points
- Communicates with `RewardsRemoteService` for data
- Implements `RewardsDashboardBusinessLogic`

### Entity (`Reward`)
- Data model representing reward items
- Includes validation and computed properties
- Codable for JSON parsing

### Router (`RewardsDashboardRouter`)
- Handles navigation to reward details
- Manages module assembly and dependency injection

## Data Flow
1. User taps refresh → View calls `presenter.didTapRefresh()`
2. Presenter calls `interactor.fetchRewards()`
3. Interactor calls `rewardsService.getRewards()`
4. Service returns data → Interactor calls `presenter.presentRewards(_)`
5. Presenter formats data → calls `view.displayRewards(_)`
6. View updates UI with formatted reward list

## Usage
```swift
// Module assembly
let module = RewardsDashboardBuilder.build()
navigationController.pushViewController(module, animated: true)
```
```

---

## API Endpoint Documentation in Remote Service

### Use Case
Use this prompt when adding documentation to functions in RemoteService or networking layers. It's important to document what each service call does, what endpoint it hits, and what data it expects/returns, especially as the number of APIs grows in a project.

### Scenario
Documenting network service functions and API integrations.

### Prompt
Document the network service functions in **[FeatureName]RemoteService**. For each public API method, write a `///` comment describing its purpose and usage. Include details such as the HTTP method and endpoint, what parameters are sent, and what the completion handler returns. Also note any important behavior like authentication requirements or retry logic. This documentation will serve as an in-code reference for developers to understand backend integrations.

### Example

```swift
/// Remote service for managing reward-related API calls
/// Handles all network communication for the rewards feature
protocol RewardsRemoteServiceProtocol {
    /// Fetches all available rewards from the server
    /// - Parameter completion: Called with Result containing rewards array or error
    func getAvailableRewards(completion: @escaping (Result<[Reward], Error>) -> Void)
    
    /// Claims a specific reward for the current user
    /// - Parameters:
    ///   - rewardId: Unique identifier of the reward to claim
    ///   - completion: Called with Result indicating success or failure
    func claimReward(_ rewardId: String, completion: @escaping (Result<Void, Error>) -> Void)
}

final class RewardsRemoteService: RewardsRemoteServiceProtocol {
    
    /// Calls GET `/api/v1/rewards` to retrieve available rewards
    /// Requires user authentication token in headers
    /// - Parameter completion: Returns parsed Reward array or NetworkError
    func getAvailableRewards(completion: @escaping (Result<[Reward], Error>) -> Void) {
        networkClient.get("/api/v1/rewards") { result in
            switch result {
            case .success(let data):
                do {
                    let rewards = try JSONDecoder().decode([Reward].self, from: data)
                    completion(.success(rewards))
                } catch {
                    completion(.failure(NetworkError.parsingFailed))
                }
            case .failure(let error):
                completion(.failure(error))
            }
        }
    }
    
    /// Calls POST `/api/v1/rewards/{id}/claim` to claim a reward
    /// Deducts points from user account if successful
    /// - Parameters:
    ///   - rewardId: The reward ID to claim
    ///   - completion: Success/failure result
    func claimReward(_ rewardId: String, completion: @escaping (Result<Void, Error>) -> Void) {
        let endpoint = "/api/v1/rewards/\(rewardId)/claim"
        networkClient.post(endpoint, body: nil) { result in
            switch result {
            case .success:
                completion(.success(()))
            case .failure(let error):
                completion(.failure(error))
            }
        }
    }
}
```

---

## Documentation Best Practices

### Swift Documentation Guidelines
- Use `///` for public APIs that will be consumed by other developers
- Use `//` for internal implementation details
- Include parameter descriptions using `- Parameter name: description`
- Document return values using `- Returns: description`
- Add `- Throws:` for methods that can throw errors

### VIPER Module Documentation
- **Protocols**: Always document protocol methods and their expected behavior
- **Data Flow**: Explain how data moves between components
- **Dependencies**: Document what each component depends on
- **Usage Examples**: Provide code samples for complex integrations

### API Documentation
- **Endpoints**: Include HTTP method and full URL path
- **Authentication**: Note any auth requirements
- **Parameters**: Document required and optional parameters
- **Response Format**: Describe expected response structure
- **Error Handling**: Document possible error scenarios 