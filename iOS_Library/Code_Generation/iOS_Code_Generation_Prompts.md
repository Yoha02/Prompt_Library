# iOS Code Generation Prompts

## Overview

This comprehensive guide provides structured prompts for generating production-ready iOS code using the VIPER (View, Interactor, Presenter, Entity, Router) architecture pattern. Each prompt is designed to ensure proper separation of concerns, maintainable code structure, and adherence to iOS development best practices.

## Architecture Principles

The VIPER architecture promotes:
- **Single Responsibility**: Each component has one clear purpose
- **Testability**: Business logic is isolated and easily testable
- **Modularity**: Components can be developed and tested independently
- **Scalability**: New features can be added without affecting existing code

## Table of Contents

1. [New VIPER Module Scaffolding](#new-viper-module-scaffolding)
2. [Interactor Business Logic Implementation](#interactor-business-logic-implementation)
3. [Presenter Data Transformation Logic](#presenter-data-transformation-logic)
4. [Router Navigation Implementation](#router-navigation-implementation)
5. [Remote Service Integration](#remote-service-integration)

---

## New VIPER Module Scaffolding

### Purpose
This prompt generates a complete VIPER module architecture from scratch, establishing the foundational structure for a new feature. It creates all necessary components with proper protocol-based communication, dependency injection setup, and clear separation of concerns.

### When to Use
- Starting development of a new feature module
- Need to establish consistent architecture patterns across the team
- Creating a template for future feature development
- Ensuring proper VIPER implementation from the beginning

### Business Value
- **Reduced Development Time**: Standardized scaffolding accelerates feature development
- **Consistency**: Ensures uniform architecture patterns across the application
- **Maintainability**: Clear separation of concerns simplifies future modifications
- **Testability**: Protocol-based design enables comprehensive unit testing

### Prompt Template
```
Generate a production-ready VIPER module in Swift for a feature called [FeatureName]. 

Requirements:
- Implement complete VIPER architecture (View, Interactor, Presenter, Entity, Router)
- Use protocol-oriented design for all component communications
- Include dependency injection setup and module builder
- Add comprehensive documentation comments
- Implement proper error handling patterns
- Include placeholder methods for common operations
- Follow iOS development best practices and naming conventions
- Organize code into logical file structure

Deliverables:
- View Controller with protocol conformance
- Business logic Interactor with protocol definitions
- Presenter with data transformation logic
- Entity models with validation
- Router with navigation methods
- Module builder for dependency injection
- Protocol definitions for all component interactions
```

### Implementation Example

**Request**: Generate a production-ready VIPER module for RewardsDashboard feature

**Generated Architecture**:

```swift
// MARK: - Entity
/// Core data model representing a reward item in the loyalty system
struct RewardItem: Codable, Equatable {
    let id: String
    let title: String
    let points: Int
    let description: String
    let imageURL: String?
    let expiryDate: Date?
    
    var isExpired: Bool {
        guard let expiryDate = expiryDate else { return false }
        return expiryDate < Date()
    }
}

// MARK: - Protocols
protocol RewardsDashboardBusinessLogic: AnyObject {
    /// Fetches available rewards from remote service
    func fetchRewards()
    /// Refreshes reward data
    func refreshRewards()
    /// Handles reward selection
    func selectReward(with id: String)
}

protocol RewardsDashboardPresentationLogic: AnyObject {
    /// Presents successfully fetched rewards
    func presentRewards(_ rewards: [RewardItem])
    /// Presents loading state
    func presentLoadingState()
    /// Presents error state
    func presentError(_ error: Error)
}

protocol RewardsDashboardDisplayLogic: AnyObject {
    /// Displays formatted reward data
    func displayRewards(_ viewModels: [RewardViewModel])
    /// Shows loading indicator
    func showLoadingState()
    /// Shows error message
    func showError(message: String)
}

protocol RewardsDashboardRoutingLogic: AnyObject {
    /// Navigates to reward details
    func routeToRewardDetails(reward: RewardItem)
}

// MARK: - View Models
struct RewardViewModel {
    let id: String
    let title: String
    let pointsText: String
    let description: String
    let imageURL: URL?
    let isExpired: Bool
    let accessibilityLabel: String
}

// MARK: - Interactor
final class RewardsDashboardInteractor {
    weak var presenter: RewardsDashboardPresentationLogic?
    private let rewardsService: RewardsServiceProtocol
    private let analyticsService: AnalyticsServiceProtocol
    
    init(rewardsService: RewardsServiceProtocol, 
         analyticsService: AnalyticsServiceProtocol) {
        self.rewardsService = rewardsService
        self.analyticsService = analyticsService
    }
}

extension RewardsDashboardInteractor: RewardsDashboardBusinessLogic {
    func fetchRewards() {
        presenter?.presentLoadingState()
        analyticsService.track(event: "rewards_fetch_started")
        
        rewardsService.fetchRewards { [weak self] result in
            DispatchQueue.main.async {
                switch result {
                case .success(let rewards):
                    self?.presenter?.presentRewards(rewards)
                case .failure(let error):
                    self?.presenter?.presentError(error)
                }
            }
        }
    }
    
    func refreshRewards() {
        fetchRewards()
    }
    
    func selectReward(with id: String) {
        analyticsService.track(event: "reward_selected", parameters: ["reward_id": id])
    }
}

// MARK: - Presenter
final class RewardsDashboardPresenter {
    weak var view: RewardsDashboardDisplayLogic?
    var router: RewardsDashboardRoutingLogic?
    
    private let dateFormatter: DateFormatter = {
        let formatter = DateFormatter()
        formatter.dateStyle = .medium
        return formatter
    }()
}

extension RewardsDashboardPresenter: RewardsDashboardPresentationLogic {
    func presentRewards(_ rewards: [RewardItem]) {
        let viewModels = rewards.map { reward in
            RewardViewModel(
                id: reward.id,
                title: reward.title,
                pointsText: "\(reward.points) points",
                description: reward.description,
                imageURL: URL(string: reward.imageURL ?? ""),
                isExpired: reward.isExpired,
                accessibilityLabel: "\(reward.title), \(reward.points) points required"
            )
        }
        view?.displayRewards(viewModels)
    }
    
    func presentLoadingState() {
        view?.showLoadingState()
    }
    
    func presentError(_ error: Error) {
        let message = error.localizedDescription
        view?.showError(message: message)
    }
}

// MARK: - Module Builder
enum RewardsDashboardModuleBuilder {
    static func build() -> UIViewController {
        let rewardsService = RewardsService()
        let analyticsService = AnalyticsService()
        
        let interactor = RewardsDashboardInteractor(
            rewardsService: rewardsService,
            analyticsService: analyticsService
        )
        
        let presenter = RewardsDashboardPresenter()
        let viewController = RewardsDashboardViewController()
        let router = RewardsDashboardRouter(viewController: viewController)
        
        // Wire dependencies
        viewController.presenter = presenter
        presenter.view = viewController
        presenter.router = router
        interactor.presenter = presenter
        
        return viewController
    }
}
```

**Key Features Generated**:
- ✅ Complete protocol-based architecture
- ✅ Dependency injection setup
- ✅ Error handling patterns
- ✅ Analytics integration points
- ✅ Accessibility support
- ✅ Thread-safe operations
- ✅ Memory management best practices

---

## Interactor Business Logic Implementation

### Purpose
This prompt facilitates the creation of robust, testable business logic within Interactor components. It ensures proper separation between business rules and presentation concerns while maintaining clean, scalable architecture patterns.

### When to Use
- Implementing new business logic requirements
- Adding data processing or validation rules
- Integrating with external services or APIs
- Creating complex business workflows
- Refactoring existing business logic for better testability

### Business Value
- **Maintainability**: Business logic is centralized and isolated from UI concerns
- **Testability**: Pure business logic can be thoroughly unit tested
- **Reusability**: Business rules can be shared across different presentation layers
- **Scalability**: New business requirements can be added without affecting UI code

### Prompt Template
```
Implement business logic in the [FeatureName]Interactor for the following requirement:

Business Requirement: [Detailed description of the business rule or process]

Technical Requirements:
- Implement method: [methodName]
- Input parameters: [parameter specifications]
- Business validation rules: [validation requirements]
- External dependencies: [services, repositories, etc.]
- Success scenarios: [expected outcomes]
- Error scenarios: [error conditions and handling]
- Performance considerations: [if applicable]

Implementation Standards:
- Use dependency injection for external services
- Implement comprehensive error handling
- Ensure thread safety for async operations
- Include proper logging for debugging
- Follow SOLID principles
- Add detailed documentation comments
- Design for unit testability

Output Format:
- Protocol definition with method signature
- Implementation with business logic
- Error handling patterns
- Integration with presenter protocol
- Unit test considerations
```

### Implementation Example

**Business Requirement**: Implement reward validation and claim processing with business rules

**Generated Implementation**:

```swift
// MARK: - Business Logic Protocol
protocol RewardClaimBusinessLogic: AnyObject {
    /// Validates if user can claim a specific reward
    /// - Parameters:
    ///   - rewardId: Unique identifier of the reward
    ///   - userId: User attempting to claim the reward
    func validateRewardClaim(rewardId: String, userId: String)
    
    /// Processes reward claim after validation
    /// - Parameters:
    ///   - rewardId: Unique identifier of the reward
    ///   - userId: User claiming the reward
    func processRewardClaim(rewardId: String, userId: String)
}

// MARK: - Business Logic Implementation
extension RewardsDashboardInteractor: RewardClaimBusinessLogic {
    
    func validateRewardClaim(rewardId: String, userId: String) {
        presenter?.presentLoadingState()
        
        // Execute validation business logic
        Task { [weak self] in
            do {
                let validationResult = try await self?.executeValidationWorkflow(
                    rewardId: rewardId, 
                    userId: userId
                )
                
                await MainActor.run {
                    switch validationResult {
                    case .valid(let reward):
                        self?.presenter?.presentClaimEligibility(
                            reward: reward, 
                            isEligible: true
                        )
                    case .invalid(let reason):
                        self?.presenter?.presentClaimEligibility(
                            reward: nil, 
                            isEligible: false, 
                            reason: reason
                        )
                    case .none:
                        self?.presenter?.presentError(
                            RewardError.validationFailed
                        )
                    }
                }
            } catch {
                await MainActor.run {
                    self?.presenter?.presentError(error)
                }
            }
        }
    }
    
    func processRewardClaim(rewardId: String, userId: String) {
        Task { [weak self] in
            do {
                // Execute claim processing workflow
                let claimResult = try await self?.executeClaimWorkflow(
                    rewardId: rewardId,
                    userId: userId
                )
                
                await MainActor.run {
                    switch claimResult {
                    case .success(let claimedReward):
                        self?.analyticsService.track(
                            event: "reward_claimed_successfully",
                            parameters: [
                                "reward_id": rewardId,
                                "user_id": userId,
                                "points_redeemed": claimedReward.pointsValue
                            ]
                        )
                        self?.presenter?.presentClaimSuccess(claimedReward)
                        
                    case .failure(let claimError):
                        self?.analyticsService.track(
                            event: "reward_claim_failed",
                            parameters: [
                                "reward_id": rewardId,
                                "error": claimError.localizedDescription
                            ]
                        )
                        self?.presenter?.presentClaimFailure(claimError)
                        
                    case .none:
                        self?.presenter?.presentError(
                            RewardError.claimProcessingFailed
                        )
                    }
                }
            } catch {
                await MainActor.run {
                    self?.presenter?.presentError(error)
                }
            }
        }
    }
    
    // MARK: - Private Business Logic Methods
    
    private func executeValidationWorkflow(
        rewardId: String, 
        userId: String
    ) async throws -> ValidationResult {
        // Step 1: Verify reward exists and is active
        guard let reward = try await rewardsRepository.findReward(by: rewardId),
              reward.isActive else {
            return .invalid(.rewardNotAvailable)
        }
        
        // Step 2: Check user eligibility
        let user = try await userRepository.findUser(by: userId)
        guard user.pointsBalance >= reward.requiredPoints else {
            return .invalid(.insufficientPoints)
        }
        
        // Step 3: Validate business rules
        guard !user.hasClaimedReward(rewardId) else {
            return .invalid(.alreadyClaimed)
        }
        
        guard reward.remainingQuantity > 0 else {
            return .invalid(.outOfStock)
        }
        
        // Step 4: Check time-based restrictions
        if let expiryDate = reward.expiryDate, expiryDate < Date() {
            return .invalid(.expired)
        }
        
        return .valid(reward)
    }
    
    private func executeClaimWorkflow(
        rewardId: String,
        userId: String
    ) async throws -> ClaimResult {
        // Execute transactional claim process
        return try await rewardsRepository.executeClaimTransaction { transaction in
            // Deduct points from user
            try await userRepository.deductPoints(
                userId: userId,
                amount: reward.requiredPoints,
                transaction: transaction
            )
            
            // Update reward inventory
            try await rewardsRepository.decrementQuantity(
                rewardId: rewardId,
                transaction: transaction
            )
            
            // Create claim record
            let claimRecord = try await claimsRepository.createClaim(
                userId: userId,
                rewardId: rewardId,
                pointsRedeemed: reward.requiredPoints,
                transaction: transaction
            )
            
            return .success(claimRecord)
        }
    }
}

// MARK: - Supporting Types
enum ValidationResult {
    case valid(Reward)
    case invalid(ValidationError)
}

enum ClaimResult {
    case success(ClaimedReward)
    case failure(ClaimError)
}

enum ValidationError {
    case rewardNotAvailable
    case insufficientPoints
    case alreadyClaimed
    case outOfStock
    case expired
}

enum ClaimError: Error {
    case transactionFailed
    case inventoryUpdateFailed
    case pointsDeductionFailed
    case networkError(Error)
}
```

**Key Implementation Features**:
- ✅ Comprehensive business rule validation
- ✅ Async/await pattern for modern Swift
- ✅ Transactional data operations
- ✅ Analytics integration
- ✅ Comprehensive error handling
- ✅ Thread-safe operations
- ✅ Testable architecture design

---

## Presenter Data Transformation Logic

### Purpose
This prompt guides the implementation of sophisticated data transformation and presentation logic within Presenter components. It ensures proper separation between raw business data and user-facing presentation formats while maintaining clean, testable architecture.

### When to Use
- Transforming business data into view-specific formats
- Implementing complex UI state management
- Creating reusable view model structures
- Handling multiple presentation scenarios for the same data
- Managing loading, error, and empty states

### Business Value
- **User Experience**: Data is presented in user-friendly, contextualized formats
- **Consistency**: Uniform data presentation across different views
- **Maintainability**: Presentation logic is centralized and easily modifiable
- **Testability**: View model transformation can be thoroughly unit tested

### Prompt Template
```
Implement presentation logic in the [FeatureName]Presenter for the following scenarios:

Data Transformation Requirements:
- Source data model: [Entity description]
- Target view model: [ViewModel specifications]
- Presentation rules: [formatting, sorting, filtering requirements]
- Localization needs: [text localization requirements]
- Accessibility features: [accessibility label and hint requirements]
- State management: [loading, error, empty state handling]

UI State Scenarios:
- Success state: [data presentation format]
- Loading state: [loading indicator requirements]
- Error state: [error message and recovery options]
- Empty state: [empty state messaging and actions]
- Partial data state: [handling incomplete data]

Implementation Standards:
- Create comprehensive view model structures
- Implement proper formatting and localization
- Handle all UI states consistently
- Include accessibility support
- Design for unit testability
- Follow iOS Human Interface Guidelines
- Implement proper error messaging

Output Format:
- View model definitions
- Presentation protocol methods
- Data transformation implementations
- State management logic
- Accessibility integration
```

### Implementation Example

**Requirement**: Implement comprehensive reward presentation logic with multiple UI states

**Generated Implementation**:

```swift
// MARK: - View Models
struct RewardListViewModel {
    let sections: [RewardSectionViewModel]
    let totalRewardsCount: Int
    let userPointsBalance: String
    let lastUpdated: String
    let isEmpty: Bool
    let accessibilityAnnouncement: String
}

struct RewardSectionViewModel {
    let title: String
    let rewards: [RewardItemViewModel]
    let sectionId: String
    let headerAccessibilityLabel: String
}

struct RewardItemViewModel: Equatable {
    let id: String
    let title: String
    let description: String
    let pointsText: String
    let formattedPointsText: NSAttributedString
    let imageURL: URL?
    let isEligible: Bool
    let statusText: String
    let statusColor: UIColor
    let expiryText: String?
    let actionButtonTitle: String
    let isActionEnabled: Bool
    let accessibilityLabel: String
    let accessibilityHint: String?
    
    // Visual state properties
    let backgroundStyle: ItemBackgroundStyle
    let badgeConfiguration: BadgeConfiguration?
    let progressValue: Float? // For point progress indicators
}

// MARK: - Supporting Types
enum ItemBackgroundStyle {
    case standard
    case premium
    case expired
    case unavailable
}

struct BadgeConfiguration {
    let text: String
    let backgroundColor: UIColor
    let textColor: UIColor
    let accessibilityLabel: String
}

// MARK: - Presentation Logic Implementation
extension RewardsDashboardPresenter: RewardsDashboardPresentationLogic {
    
    func presentRewards(_ rewards: [Reward], userContext: UserContext) {
        let viewModel = createRewardListViewModel(
            from: rewards,
            userContext: userContext
        )
        
        view?.displayRewards(viewModel)
        
        // Track presentation analytics
        analyticsTracker?.track(
            event: "rewards_presented",
            parameters: [
                "total_rewards": rewards.count,
                "eligible_rewards": rewards.filter { isEligible($0, for: userContext) }.count,
                "user_points": userContext.pointsBalance
            ]
        )
    }
    
    func presentLoadingState() {
        let loadingViewModel = LoadingViewModel(
            message: LocalizedStrings.Rewards.loadingMessage,
            accessibilityLabel: LocalizedStrings.Accessibility.Rewards.loading
        )
        view?.showLoadingState(loadingViewModel)
    }
    
    func presentError(_ error: Error) {
        let errorViewModel = createErrorViewModel(from: error)
        view?.showError(errorViewModel)
        
        // Track error analytics
        analyticsTracker?.track(
            event: "rewards_error_presented",
            parameters: [
                "error_type": String(describing: type(of: error)),
                "error_description": error.localizedDescription
            ]
        )
    }
    
    func presentEmptyState(reason: EmptyStateReason) {
        let emptyViewModel = createEmptyStateViewModel(for: reason)
        view?.showEmptyState(emptyViewModel)
    }
    
    func presentRewardClaimResult(_ result: ClaimResult) {
        switch result {
        case .success(let claimedReward):
            let successViewModel = ClaimSuccessViewModel(
                title: LocalizedStrings.Rewards.claimSuccessTitle,
                message: String(
                    format: LocalizedStrings.Rewards.claimSuccessMessage,
                    claimedReward.title
                ),
                pointsDeducted: formatPoints(claimedReward.pointsRedeemed),
                actionTitle: LocalizedStrings.Common.continue
            )
            view?.showClaimSuccess(successViewModel)
            
        case .failure(let error):
            let errorViewModel = createClaimErrorViewModel(from: error)
            view?.showClaimError(errorViewModel)
        }
    }
    
    // MARK: - Private Data Transformation Methods
    
    private func createRewardListViewModel(
        from rewards: [Reward],
        userContext: UserContext
    ) -> RewardListViewModel {
        
        // Group rewards by category
        let groupedRewards = Dictionary(grouping: rewards) { $0.category }
        
        // Create sections with sorted rewards
        let sections = groupedRewards.map { category, categoryRewards in
            let sortedRewards = categoryRewards.sorted { 
                prioritizeReward($0, over: $1, for: userContext) 
            }
            
            let rewardViewModels = sortedRewards.map { 
                createRewardItemViewModel(from: $0, userContext: userContext)
            }
            
            return RewardSectionViewModel(
                title: category.displayName,
                rewards: rewardViewModels,
                sectionId: category.identifier,
                headerAccessibilityLabel: String(
                    format: LocalizedStrings.Accessibility.Rewards.sectionHeader,
                    category.displayName,
                    rewardViewModels.count
                )
            )
        }.sorted { $0.title < $1.title }
        
        return RewardListViewModel(
            sections: sections,
            totalRewardsCount: rewards.count,
            userPointsBalance: formatPoints(userContext.pointsBalance),
            lastUpdated: formatLastUpdated(Date()),
            isEmpty: rewards.isEmpty,
            accessibilityAnnouncement: createAccessibilityAnnouncement(
                for: rewards,
                userContext: userContext
            )
        )
    }
    
    private func createRewardItemViewModel(
        from reward: Reward,
        userContext: UserContext
    ) -> RewardItemViewModel {
        
        let isEligible = isEligible(reward, for: userContext)
        let statusInfo = determineStatusInfo(for: reward, userContext: userContext)
        
        return RewardItemViewModel(
            id: reward.id,
            title: reward.title,
            description: reward.description,
            pointsText: formatPoints(reward.requiredPoints),
            formattedPointsText: createAttributedPointsText(
                points: reward.requiredPoints,
                isEligible: isEligible
            ),
            imageURL: URL(string: reward.imageURL ?? ""),
            isEligible: isEligible,
            statusText: statusInfo.text,
            statusColor: statusInfo.color,
            expiryText: formatExpiryDate(reward.expiryDate),
            actionButtonTitle: determineActionTitle(for: reward, isEligible: isEligible),
            isActionEnabled: isEligible && !reward.isExpired,
            accessibilityLabel: createAccessibilityLabel(for: reward, isEligible: isEligible),
            accessibilityHint: createAccessibilityHint(for: reward, isEligible: isEligible),
            backgroundStyle: determineBackgroundStyle(for: reward, isEligible: isEligible),
            badgeConfiguration: createBadgeConfiguration(for: reward),
            progressValue: calculateProgressValue(for: reward, userContext: userContext)
        )
    }
    
    private func isEligible(_ reward: Reward, for userContext: UserContext) -> Bool {
        return userContext.pointsBalance >= reward.requiredPoints &&
               !reward.isExpired &&
               reward.remainingQuantity > 0 &&
               !userContext.claimedRewardIds.contains(reward.id)
    }
    
    private func formatPoints(_ points: Int) -> String {
        let formatter = NumberFormatter()
        formatter.numberStyle = .decimal
        formatter.groupingSeparator = ","
        
        let formattedNumber = formatter.string(from: NSNumber(value: points)) ?? "\(points)"
        return String(format: LocalizedStrings.Rewards.pointsFormat, formattedNumber)
    }
    
    private func createAttributedPointsText(
        points: Int, 
        isEligible: Bool
    ) -> NSAttributedString {
        let pointsText = formatPoints(points)
        let attributes: [NSAttributedString.Key: Any] = [
            .font: UIFont.systemFont(ofSize: 16, weight: .semibold),
            .foregroundColor: isEligible ? UIColor.systemBlue : UIColor.systemGray
        ]
        
        return NSAttributedString(string: pointsText, attributes: attributes)
    }
    
    private func createAccessibilityLabel(
        for reward: Reward, 
        isEligible: Bool
    ) -> String {
        let eligibilityText = isEligible 
            ? LocalizedStrings.Accessibility.Rewards.eligible
            : LocalizedStrings.Accessibility.Rewards.notEligible
            
        return String(
            format: LocalizedStrings.Accessibility.Rewards.rewardLabel,
            reward.title,
            formatPoints(reward.requiredPoints),
            eligibilityText
        )
    }
    
    private func createErrorViewModel(from error: Error) -> ErrorViewModel {
        let errorInfo = ErrorMapper.mapToUserFriendlyError(error)
        
        return ErrorViewModel(
            title: errorInfo.title,
            message: errorInfo.message,
            primaryActionTitle: errorInfo.primaryAction?.title,
            secondaryActionTitle: errorInfo.secondaryAction?.title,
            icon: errorInfo.iconName,
            accessibilityLabel: String(
                format: LocalizedStrings.Accessibility.Error.label,
                errorInfo.title,
                errorInfo.message
            )
        )
    }
}

// MARK: - Supporting Enums and Structs
enum EmptyStateReason {
    case noRewards
    case allRewardsExpired
    case insufficientPoints
    case networkError
}

struct StatusInfo {
    let text: String
    let color: UIColor
}

struct LoadingViewModel {
    let message: String
    let accessibilityLabel: String
}

struct ErrorViewModel {
    let title: String
    let message: String
    let primaryActionTitle: String?
    let secondaryActionTitle: String?
    let icon: String?
    let accessibilityLabel: String
}

struct ClaimSuccessViewModel {
    let title: String
    let message: String
    let pointsDeducted: String
    let actionTitle: String
}
```

**Key Implementation Features**:
- ✅ Comprehensive view model architecture
- ✅ Advanced data transformation logic
- ✅ Complete UI state management
- ✅ Accessibility integration
- ✅ Localization support
- ✅ Analytics integration
- ✅ Error handling and recovery
- ✅ Performance-optimized formatting

---

## Router Navigation Implementation

### Purpose
This prompt enables the creation of sophisticated navigation and routing logic within Router components, ensuring clean separation of navigation concerns from business logic while maintaining flexible, testable navigation patterns.

### When to Use
- Implementing complex navigation flows between modules
- Creating conditional navigation based on user state
- Setting up deep linking and universal link handling
- Managing navigation stack and modal presentations
- Implementing tab-based and drawer navigation patterns

### Business Value
- **User Experience**: Smooth, intuitive navigation flows
- **Maintainability**: Navigation logic is centralized and easily modifiable  
- **Flexibility**: Easy to adapt navigation patterns for different user flows
- **Testability**: Navigation logic can be isolated and unit tested

### Prompt Template
```
Implement navigation logic in the [FeatureName]Router for the following requirements:

Navigation Requirements:
- Source module: [OriginFeature] 
- Target module: [DestinationFeature]
- Navigation trigger: [user action or business event]
- Navigation style: [push, present, modal, sheet, etc.]
- Data passing: [parameters to pass between modules]
- Animation requirements: [custom transitions if needed]
- Back navigation: [navigation stack management]

Conditional Navigation:
- User state considerations: [authentication, permissions, etc.]
- Business rule validations: [eligibility checks, prerequisites]
- Error handling: [navigation failure scenarios]
- Deep linking support: [URL handling capabilities]

Implementation Standards:
- Use dependency injection for module assembly
- Implement proper data passing mechanisms
- Handle navigation state management
- Include analytics tracking for navigation events
- Support accessibility navigation
- Design for unit testability
- Follow iOS navigation patterns

Output Format:
- Router protocol definitions
- Navigation method implementations
- Module builder integrations
- Data passing mechanisms
- Error handling patterns
```

### Implementation Example

**Requirement**: Implement comprehensive navigation system for rewards flow with conditional routing

**Generated Implementation**:

```swift
// MARK: - Router Protocol
protocol RewardsDashboardRoutingLogic: AnyObject {
    /// Navigates to reward details with comprehensive context
    func routeToRewardDetails(
        reward: Reward,
        userContext: UserContext,
        source: NavigationSource
    )
    
    /// Navigates to claim confirmation flow
    func routeToClaimConfirmation(
        reward: Reward,
        userContext: UserContext
    )
    
    /// Navigates to points purchase flow
    func routeToPurchasePoints(
        requiredPoints: Int,
        currentPoints: Int
    )
    
    /// Handles authentication requirement navigation
    func routeToAuthentication(
        completion: @escaping (Bool) -> Void
    )
    
    /// Dismisses current module with completion
    func dismissModule(
        animated: Bool,
        completion: (() -> Void)?
    )
}

// MARK: - Router Implementation
final class RewardsDashboardRouter {
    weak var viewController: UIViewController?
    private let analyticsTracker: AnalyticsTracking
    private let authenticationService: AuthenticationService
    private let navigationCoordinator: NavigationCoordinating
    
    init(
        viewController: UIViewController,
        analyticsTracker: AnalyticsTracking,
        authenticationService: AuthenticationService,
        navigationCoordinator: NavigationCoordinating
    ) {
        self.viewController = viewController
        self.analyticsTracker = analyticsTracker
        self.authenticationService = authenticationService
        self.navigationCoordinator = navigationCoordinator
    }
}

extension RewardsDashboardRouter: RewardsDashboardRoutingLogic {
    
    func routeToRewardDetails(
        reward: Reward,
        userContext: UserContext,
        source: NavigationSource
    ) {
        // Track navigation analytics
        analyticsTracker.track(
            event: "navigation_reward_details",
            parameters: [
                "reward_id": reward.id,
                "source": source.rawValue,
                "user_eligible": userContext.pointsBalance >= reward.requiredPoints
            ]
        )
        
        // Build destination module with dependencies
        let detailModule = RewardDetailModuleBuilder.build(
            reward: reward,
            userContext: userContext,
            navigationDelegate: self
        )
        
        // Configure navigation presentation
        let navigationConfiguration = NavigationConfiguration(
            presentationStyle: .push,
            transitionStyle: .slide,
            shouldHideTabBar: true,
            backButtonTitle: LocalizedStrings.Navigation.back
        )
        
        // Execute navigation
        navigationCoordinator.navigate(
            from: viewController,
            to: detailModule,
            configuration: navigationConfiguration
        ) { [weak self] success in
            if success {
                self?.handleSuccessfulNavigation(to: .rewardDetails)
            } else {
                self?.handleNavigationFailure(.rewardDetailsUnavailable)
            }
        }
    }
    
    func routeToClaimConfirmation(
        reward: Reward,
        userContext: UserContext
    ) {
        // Validate user can proceed with claim
        guard validateClaimEligibility(reward: reward, userContext: userContext) else {
            handleIneligibleClaim(reward: reward, userContext: userContext)
            return
        }
        
        // Build claim confirmation module
        let claimModule = ClaimConfirmationModuleBuilder.build(
            reward: reward,
            userContext: userContext,
            delegate: self
        )
        
        // Present as modal sheet
        let presentationConfiguration = ModalPresentationConfiguration(
            presentationStyle: .pageSheet,
            detents: [.medium(), .large()],
            isModalInPresentation: true,
            shouldShowGrabber: true
        )
        
        navigationCoordinator.presentModal(
            from: viewController,
            module: claimModule,
            configuration: presentationConfiguration
        )
        
        // Track claim flow initiation
        analyticsTracker.track(
            event: "claim_confirmation_presented",
            parameters: [
                "reward_id": reward.id,
                "required_points": reward.requiredPoints,
                "user_points": userContext.pointsBalance
            ]
        )
    }
    
    func routeToPurchasePoints(
        requiredPoints: Int,
        currentPoints: Int
    ) {
        let shortfall = max(0, requiredPoints - currentPoints)
        
        // Build purchase points module
        let purchaseModule = PointsPurchaseModuleBuilder.build(
            minimumPurchase: shortfall,
            currentBalance: currentPoints,
            purchaseDelegate: self
        )
        
        // Present with custom transition
        let transitionConfiguration = TransitionConfiguration(
            presentationStyle: .formSheet,
            transitionStyle: .coverVertical,
            shouldDimBackground: true
        )
        
        navigationCoordinator.presentWithTransition(
            from: viewController,
            to: purchaseModule,
            configuration: transitionConfiguration
        )
        
        analyticsTracker.track(
            event: "points_purchase_initiated",
            parameters: [
                "points_shortfall": shortfall,
                "current_points": currentPoints
            ]
        )
    }
    
    func routeToAuthentication(
        completion: @escaping (Bool) -> Void
    ) {
        guard !authenticationService.isAuthenticated else {
            completion(true)
            return
        }
        
        let authModule = AuthenticationModuleBuilder.build(
            authenticationReason: .rewardAccess,
            completion: { [weak self] result in
                DispatchQueue.main.async {
                    completion(result.isAuthenticated)
                    
                    self?.analyticsTracker.track(
                        event: "authentication_completed",
                        parameters: [
                            "success": result.isAuthenticated,
                            "method": result.authenticationMethod?.rawValue ?? "unknown"
                        ]
                    )
                }
            }
        )
        
        navigationCoordinator.presentModal(
            from: viewController,
            module: authModule,
            configuration: .fullScreenModal
        )
    }
    
    func dismissModule(
        animated: Bool = true,
        completion: (() -> Void)? = nil
    ) {
        navigationCoordinator.dismiss(
            from: viewController,
            animated: animated,
            completion: completion
        )
    }
    
    // MARK: - Private Navigation Helpers
    
    private func validateClaimEligibility(
        reward: Reward,
        userContext: UserContext
    ) -> Bool {
        return userContext.pointsBalance >= reward.requiredPoints &&
               !reward.isExpired &&
               reward.remainingQuantity > 0 &&
               !userContext.claimedRewardIds.contains(reward.id)
    }
    
    private func handleIneligibleClaim(
        reward: Reward,
        userContext: UserContext
    ) {
        let pointsShortfall = reward.requiredPoints - userContext.pointsBalance
        
        if pointsShortfall > 0 {
            presentInsufficientPointsAlert(
                requiredPoints: reward.requiredPoints,
                currentPoints: userContext.pointsBalance,
                shortfall: pointsShortfall
            )
        } else if reward.isExpired {
            presentRewardExpiredAlert(reward: reward)
        } else if reward.remainingQuantity <= 0 {
            presentRewardUnavailableAlert(reward: reward)
        }
    }
    
    private func presentInsufficientPointsAlert(
        requiredPoints: Int,
        currentPoints: Int,
        shortfall: Int
    ) {
        let alertConfig = AlertConfiguration(
            title: LocalizedStrings.Alerts.insufficientPointsTitle,
            message: String(
                format: LocalizedStrings.Alerts.insufficientPointsMessage,
                shortfall
            ),
            primaryAction: AlertAction(
                title: LocalizedStrings.Alerts.purchasePoints,
                style: .default
            ) { [weak self] in
                self?.routeToPurchasePoints(
                    requiredPoints: requiredPoints,
                    currentPoints: currentPoints
                )
            },
            secondaryAction: AlertAction(
                title: LocalizedStrings.Common.cancel,
                style: .cancel
            )
        )
        
        navigationCoordinator.presentAlert(
            from: viewController,
            configuration: alertConfig
        )
    }
    
    private func handleSuccessfulNavigation(to destination: NavigationDestination) {
        analyticsTracker.track(
            event: "navigation_successful",
            parameters: ["destination": destination.rawValue]
        )
    }
    
    private func handleNavigationFailure(_ error: NavigationError) {
        analyticsTracker.track(
            event: "navigation_failed",
            parameters: ["error": error.localizedDescription]
        )
        
        // Present user-friendly error message
        let errorAlert = AlertConfiguration(
            title: LocalizedStrings.Errors.navigationFailedTitle,
            message: error.userFriendlyMessage,
            primaryAction: AlertAction(
                title: LocalizedStrings.Common.ok,
                style: .default
            )
        )
        
        navigationCoordinator.presentAlert(
            from: viewController,
            configuration: errorAlert
        )
    }
}

// MARK: - Navigation Delegates
extension RewardsDashboardRouter: RewardDetailNavigationDelegate {
    func rewardDetailDidRequestClaim(_ reward: Reward, userContext: UserContext) {
        routeToClaimConfirmation(reward: reward, userContext: userContext)
    }
    
    func rewardDetailDidComplete() {
        navigationCoordinator.popToRoot(animated: true)
    }
}

extension RewardsDashboardRouter: ClaimConfirmationDelegate {
    func claimConfirmationDidComplete(result: ClaimResult) {
        dismissModule { [weak self] in
            switch result {
            case .success:
                self?.handleSuccessfulClaim()
            case .failure(let error):
                self?.handleClaimFailure(error)
            }
        }
    }
}

extension RewardsDashboardRouter: PointsPurchaseDelegate {
    func pointsPurchaseDidComplete(purchasedPoints: Int) {
        dismissModule { [weak self] in
            self?.handlePointsPurchaseComplete(purchasedPoints: purchasedPoints)
        }
    }
}

// MARK: - Supporting Types
enum NavigationSource: String {
    case rewardList = "reward_list"
    case searchResults = "search_results"
    case recommendation = "recommendation"
    case deepLink = "deep_link"
}

enum NavigationDestination: String {
    case rewardDetails = "reward_details"
    case claimConfirmation = "claim_confirmation"
    case pointsPurchase = "points_purchase"
    case authentication = "authentication"
}

enum NavigationError: Error {
    case rewardDetailsUnavailable
    case authenticationRequired
    case networkConnectionRequired
    case moduleBuilderFailure
    
    var userFriendlyMessage: String {
        switch self {
        case .rewardDetailsUnavailable:
            return LocalizedStrings.Errors.rewardDetailsUnavailable
        case .authenticationRequired:
            return LocalizedStrings.Errors.authenticationRequired
        case .networkConnectionRequired:
            return LocalizedStrings.Errors.networkRequired
        case .moduleBuilderFailure:
            return LocalizedStrings.Errors.systemError
        }
    }
}

struct NavigationConfiguration {
    let presentationStyle: NavigationStyle
    let transitionStyle: TransitionStyle
    let shouldHideTabBar: Bool
    let backButtonTitle: String?
}

struct AlertConfiguration {
    let title: String
    let message: String
    let primaryAction: AlertAction
    let secondaryAction: AlertAction?
}

struct AlertAction {
    let title: String
    let style: UIAlertAction.Style
    let handler: (() -> Void)?
}
```

**Key Navigation Features**:
- ✅ Comprehensive routing protocol design
- ✅ Conditional navigation with business rules
- ✅ Advanced presentation and transition handling
- ✅ Deep analytics integration
- ✅ Error handling and recovery flows
- ✅ Accessibility and localization support
- ✅ Delegate-based completion handling
- ✅ Testable navigation architecture

---

## Remote Service Integration

### Purpose
This prompt facilitates the creation of robust, scalable remote service integrations that abstract network communication details while providing clean, testable interfaces for business logic components. It ensures proper separation between networking concerns and business logic.

### When to Use
- Integrating with RESTful APIs and GraphQL endpoints
- Implementing authentication and authorization flows
- Creating data synchronization and caching mechanisms
- Building offline-capable service layers
- Setting up real-time communication channels

### Business Value
- **Reliability**: Robust error handling and retry mechanisms
- **Performance**: Efficient data fetching and caching strategies
- **Security**: Proper authentication and data encryption
- **Maintainability**: Clean abstraction over network complexities
- **Testability**: Mockable interfaces for comprehensive testing

### Prompt Template
```
Implement a remote service for [FeatureName] with the following specifications:

API Integration Requirements:
- Base URL: [API base URL]
- Endpoints: [list of endpoints with HTTP methods]
- Authentication: [authentication mechanism - OAuth, API key, etc.]
- Request/Response format: [JSON, XML, Protocol Buffers, etc.]
- Rate limiting: [API rate limit considerations]
- Caching strategy: [cache requirements and TTL]

Data Models:
- Request models: [input parameter structures]
- Response models: [API response structures]
- Entity mappings: [business entity transformations]
- Error models: [API error response handling]

Quality Requirements:
- Error handling: [network, parsing, business logic errors]
- Retry logic: [retry strategies and backoff policies]
- Timeout configuration: [request timeout settings]
- Offline support: [caching and offline data strategies]
- Analytics tracking: [service call monitoring]
- Security measures: [data encryption, certificate pinning]

Implementation Standards:
- Use protocol-oriented design for testability
- Implement comprehensive error handling
- Add proper logging and analytics
- Support both async/await and completion handlers
- Include network reachability checking
- Design for unit testing with mock services
- Follow iOS networking best practices

Output Format:
- Service protocol definitions
- Implementation with error handling
- Request/Response model structures
- Caching and offline support
- Security and authentication integration
- Analytics and logging integration
```

### Implementation Example

**Requirement**: Implement comprehensive rewards service with caching, authentication, and offline support

**Generated Implementation**:

```swift
// MARK: - Service Protocol
protocol RewardsServiceProtocol: AnyObject {
    /// Fetches available rewards with caching support
    func fetchRewards(
        forceRefresh: Bool,
        completion: @escaping (Result<[Reward], ServiceError>) -> Void
    )
    
    /// Claims a specific reward with transaction safety
    func claimReward(
        rewardId: String,
        userId: String,
        completion: @escaping (Result<ClaimResponse, ServiceError>) -> Void
    )
    
    /// Fetches user's reward history with pagination
    func fetchRewardHistory(
        userId: String,
        page: Int,
        pageSize: Int,
        completion: @escaping (Result<RewardHistoryResponse, ServiceError>) -> Void
    )
    
    /// Modern async/await interfaces
    func fetchRewards(forceRefresh: Bool) async throws -> [Reward]
    func claimReward(rewardId: String, userId: String) async throws -> ClaimResponse
    func fetchRewardHistory(userId: String, page: Int, pageSize: Int) async throws -> RewardHistoryResponse
}

// MARK: - Service Implementation
final class RewardsService: RewardsServiceProtocol {
    
    // MARK: - Dependencies
    private let networkClient: NetworkClientProtocol
    private let cacheManager: CacheManagerProtocol
    private let authenticationService: AuthenticationServiceProtocol
    private let analyticsTracker: AnalyticsTracking
    private let reachabilityService: ReachabilityServiceProtocol
    private let securityManager: SecurityManagerProtocol
    
    // MARK: - Configuration
    private let baseURL: String
    private let requestTimeout: TimeInterval
    private let maxRetryAttempts: Int
    private let cacheTTL: TimeInterval
    
    // MARK: - Private Properties
    private let requestQueue = DispatchQueue(label: "com.app.rewards.requests", qos: .userInitiated)
    private let jsonDecoder: JSONDecoder
    private let jsonEncoder: JSONEncoder
    
    init(
        networkClient: NetworkClientProtocol,
        cacheManager: CacheManagerProtocol,
        authenticationService: AuthenticationServiceProtocol,
        analyticsTracker: AnalyticsTracking,
        reachabilityService: ReachabilityServiceProtocol,
        securityManager: SecurityManagerProtocol,
        configuration: ServiceConfiguration
    ) {
        self.networkClient = networkClient
        self.cacheManager = cacheManager
        self.authenticationService = authenticationService
        self.analyticsTracker = analyticsTracker
        self.reachabilityService = reachabilityService
        self.securityManager = securityManager
        
        self.baseURL = configuration.baseURL
        self.requestTimeout = configuration.requestTimeout
        self.maxRetryAttempts = configuration.maxRetryAttempts
        self.cacheTTL = configuration.cacheTTL
        
        // Configure JSON processing
        self.jsonDecoder = JSONDecoder()
        self.jsonDecoder.dateDecodingStrategy = .iso8601
        self.jsonDecoder.keyDecodingStrategy = .convertFromSnakeCase
        
        self.jsonEncoder = JSONEncoder()
        self.jsonEncoder.dateEncodingStrategy = .iso8601
        self.jsonEncoder.keyEncodingStrategy = .convertToSnakeCase
    }
    
    // MARK: - Public Interface Implementation
    
    func fetchRewards(
        forceRefresh: Bool = false,
        completion: @escaping (Result<[Reward], ServiceError>) -> Void
    ) {
        let cacheKey = "rewards_list"
        
        // Check cache first unless force refresh requested
        if !forceRefresh, let cachedRewards: [Reward] = cacheManager.object(forKey: cacheKey) {
            analyticsTracker.track(event: "rewards_cache_hit")
            completion(.success(cachedRewards))
            return
        }
        
        // Check network reachability
        guard reachabilityService.isReachable else {
            // Try to return stale cache data if available
            if let staleRewards: [Reward] = cacheManager.object(forKey: cacheKey, ignoringExpiry: true) {
                analyticsTracker.track(event: "rewards_offline_fallback")
                completion(.success(staleRewards))
                return
            }
            completion(.failure(.networkUnavailable))
            return
        }
        
        // Build request
        let request = RewardsListRequest()
        
        // Execute request with retry logic
        executeRequest(
            endpoint: .rewardsList,
            request: request,
            responseType: RewardsListResponse.self,
            completion: { [weak self] result in
                switch result {
                case .success(let response):
                    let rewards = response.rewards.map { $0.toEntity() }
                    
                    // Cache successful response
                    self?.cacheManager.setObject(
                        rewards,
                        forKey: cacheKey,
                        ttl: self?.cacheTTL ?? 300
                    )
                    
                    self?.analyticsTracker.track(
                        event: "rewards_fetch_success",
                        parameters: ["count": rewards.count]
                    )
                    
                    completion(.success(rewards))
                    
                case .failure(let error):
                    self?.analyticsTracker.track(
                        event: "rewards_fetch_failure",
                        parameters: ["error": error.analyticsDescription]
                    )
                    completion(.failure(error))
                }
            }
        )
    }
    
    func claimReward(
        rewardId: String,
        userId: String,
        completion: @escaping (Result<ClaimResponse, ServiceError>) -> Void
    ) {
        // Validate inputs
        guard !rewardId.isEmpty, !userId.isEmpty else {
            completion(.failure(.invalidRequest("Invalid reward or user ID")))
            return
        }
        
        // Check authentication
        guard authenticationService.isAuthenticated else {
            completion(.failure(.authenticationRequired))
            return
        }
        
        // Build request
        let request = ClaimRewardRequest(
            rewardId: rewardId,
            userId: userId,
            timestamp: Date(),
            nonce: UUID().uuidString
        )
        
        // Execute request with enhanced security
        executeSecureRequest(
            endpoint: .claimReward(rewardId: rewardId),
            request: request,
            responseType: ClaimRewardResponse.self,
            requiresAuthentication: true,
            completion: { [weak self] result in
                switch result {
                case .success(let response):
                    let claimResponse = ClaimResponse(
                        transactionId: response.transactionId,
                        pointsDeducted: response.pointsDeducted,
                        newBalance: response.newBalance,
                        claimTimestamp: response.claimTimestamp
                    )
                    
                    // Invalidate relevant caches
                    self?.invalidateRewardsCaches()
                    
                    self?.analyticsTracker.track(
                        event: "reward_claim_success",
                        parameters: [
                            "reward_id": rewardId,
                            "points_deducted": response.pointsDeducted,
                            "transaction_id": response.transactionId
                        ]
                    )
                    
                    completion(.success(claimResponse))
                    
                case .failure(let error):
                    self?.analyticsTracker.track(
                        event: "reward_claim_failure",
                        parameters: [
                            "reward_id": rewardId,
                            "error": error.analyticsDescription
                        ]
                    )
                    completion(.failure(error))
                }
            }
        )
    }
    
    func fetchRewardHistory(
        userId: String,
        page: Int = 0,
        pageSize: Int = 20,
        completion: @escaping (Result<RewardHistoryResponse, ServiceError>) -> Void
    ) {
        let request = RewardHistoryRequest(
            userId: userId,
            page: page,
            pageSize: pageSize
        )
        
        executeRequest(
            endpoint: .rewardHistory(userId: userId),
            request: request,
            responseType: RewardHistoryAPIResponse.self,
            completion: { result in
                switch result {
                case .success(let response):
                    let historyResponse = RewardHistoryResponse(
                        claims: response.claims.map { $0.toEntity() },
                        totalCount: response.totalCount,
                        hasMorePages: response.hasMorePages,
                        currentPage: response.currentPage
                    )
                    completion(.success(historyResponse))
                    
                case .failure(let error):
                    completion(.failure(error))
                }
            }
        )
    }
    
    // MARK: - Async/Await Interface
    
    func fetchRewards(forceRefresh: Bool = false) async throws -> [Reward] {
        return try await withCheckedThrowingContinuation { continuation in
            fetchRewards(forceRefresh: forceRefresh) { result in
                continuation.resume(with: result)
            }
        }
    }
    
    func claimReward(rewardId: String, userId: String) async throws -> ClaimResponse {
        return try await withCheckedThrowingContinuation { continuation in
            claimReward(rewardId: rewardId, userId: userId) { result in
                continuation.resume(with: result)
            }
        }
    }
    
    func fetchRewardHistory(userId: String, page: Int, pageSize: Int) async throws -> RewardHistoryResponse {
        return try await withCheckedThrowingContinuation { continuation in
            fetchRewardHistory(userId: userId, page: page, pageSize: pageSize) { result in
                continuation.resume(with: result)
            }
        }
    }
    
    // MARK: - Private Request Execution
    
    private func executeRequest<T: Codable, R: Codable>(
        endpoint: APIEndpoint,
        request: T,
        responseType: R.Type,
        completion: @escaping (Result<R, ServiceError>) -> Void
    ) {
        executeRequestWithRetry(
            endpoint: endpoint,
            request: request,
            responseType: responseType,
            attempt: 1,
            completion: completion
        )
    }
    
    private func executeSecureRequest<T: Codable, R: Codable>(
        endpoint: APIEndpoint,
        request: T,
        responseType: R.Type,
        requiresAuthentication: Bool = true,
        completion: @escaping (Result<R, ServiceError>) -> Void
    ) {
        // Add request signing and additional security measures
        let secureRequest = securityManager.signRequest(request)
        
        executeRequest(
            endpoint: endpoint,
            request: secureRequest,
            responseType: responseType,
            completion: completion
        )
    }
    
    private func executeRequestWithRetry<T: Codable, R: Codable>(
        endpoint: APIEndpoint,
        request: T,
        responseType: R.Type,
        attempt: Int,
        completion: @escaping (Result<R, ServiceError>) -> Void
    ) {
        // Build HTTP request
        guard let httpRequest = buildHTTPRequest(endpoint: endpoint, request: request) else {
            completion(.failure(.invalidRequest("Failed to build HTTP request")))
            return
        }
        
        // Execute network request
        networkClient.execute(request: httpRequest) { [weak self] result in
            switch result {
            case .success(let data):
                do {
                    let response = try self?.jsonDecoder.decode(responseType, from: data)
                    completion(.success(response!))
                } catch {
                    if attempt < self?.maxRetryAttempts ?? 1 {
                        self?.executeRequestWithRetry(
                            endpoint: endpoint,
                            request: request,
                            responseType: responseType,
                            attempt: attempt + 1,
                            completion: completion
                        )
                    } else {
                        completion(.failure(.parsingError(error)))
                    }
                }
                
            case .failure(let networkError):
                // Implement retry logic for recoverable errors
                if self?.shouldRetry(error: networkError, attempt: attempt) == true {
                    let delay = self?.calculateBackoffDelay(attempt: attempt) ?? 1.0
                    
                    DispatchQueue.global().asyncAfter(deadline: .now() + delay) {
                        self?.executeRequestWithRetry(
                            endpoint: endpoint,
                            request: request,
                            responseType: responseType,
                            attempt: attempt + 1,
                            completion: completion
                        )
                    }
                } else {
                    completion(.failure(.networkError(networkError)))
                }
            }
        }
    }
    
    private func buildHTTPRequest<T: Codable>(
        endpoint: APIEndpoint,
        request: T
    ) -> HTTPRequest? {
        guard let url = URL(string: baseURL + endpoint.path) else {
            return nil
        }
        
        var httpRequest = HTTPRequest(url: url)
        httpRequest.method = endpoint.method
        httpRequest.timeoutInterval = requestTimeout
        
        // Add authentication headers
        if let authToken = authenticationService.authToken {
            httpRequest.addHeader("Authorization", value: "Bearer \(authToken)")
        }
        
        // Add common headers
        httpRequest.addHeader("Content-Type", value: "application/json")
        httpRequest.addHeader("Accept", value: "application/json")
        httpRequest.addHeader("User-Agent", value: buildUserAgent())
        
        // Add request body for POST/PUT requests
        if endpoint.method != .GET {
            do {
                httpRequest.body = try jsonEncoder.encode(request)
            } catch {
                return nil
            }
        }
        
        return httpRequest
    }
    
    private func shouldRetry(error: NetworkError, attempt: Int) -> Bool {
        guard attempt < maxRetryAttempts else { return false }
        
        switch error {
        case .temporaryFailure, .timeout, .serverError(500...599):
            return true
        default:
            return false
        }
    }
    
    private func calculateBackoffDelay(attempt: Int) -> TimeInterval {
        // Exponential backoff with jitter
        let baseDelay = 1.0
        let exponentialDelay = baseDelay * pow(2.0, Double(attempt - 1))
        let jitter = Double.random(in: 0...0.1)
        return min(exponentialDelay + jitter, 30.0) // Max 30 seconds
    }
    
    private func invalidateRewardsCaches() {
        cacheManager.removeObject(forKey: "rewards_list")
        // Invalidate other related caches
    }
    
    private func buildUserAgent() -> String {
        let appVersion = Bundle.main.infoDictionary?["CFBundleShortVersionString"] as? String ?? "1.0"
        let systemVersion = UIDevice.current.systemVersion
        return "RewardsApp/\(appVersion) iOS/\(systemVersion)"
    }
}

// MARK: - Supporting Types

struct ServiceConfiguration {
    let baseURL: String
    let requestTimeout: TimeInterval
    let maxRetryAttempts: Int
    let cacheTTL: TimeInterval
}

enum APIEndpoint {
    case rewardsList
    case claimReward(rewardId: String)
    case rewardHistory(userId: String)
    
    var path: String {
        switch self {
        case .rewardsList:
            return "/api/v1/rewards"
        case .claimReward(let rewardId):
            return "/api/v1/rewards/\(rewardId)/claim"
        case .rewardHistory(let userId):
            return "/api/v1/users/\(userId)/reward-history"
        }
    }
    
    var method: HTTPMethod {
        switch self {
        case .rewardsList, .rewardHistory:
            return .GET
        case .claimReward:
            return .POST
        }
    }
}

enum ServiceError: Error {
    case networkUnavailable
    case authenticationRequired
    case invalidRequest(String)
    case networkError(NetworkError)
    case parsingError(Error)
    case businessLogicError(String)
    case rateLimitExceeded
    case serverMaintenance
    
    var analyticsDescription: String {
        switch self {
        case .networkUnavailable:
            return "network_unavailable"
        case .authenticationRequired:
            return "authentication_required"
        case .invalidRequest:
            return "invalid_request"
        case .networkError:
            return "network_error"
        case .parsingError:
            return "parsing_error"
        case .businessLogicError:
            return "business_logic_error"
        case .rateLimitExceeded:
            return "rate_limit_exceeded"
        case .serverMaintenance:
            return "server_maintenance"
        }
    }
}

// Request/Response Models
struct RewardsListRequest: Codable {
    let timestamp: Date = Date()
}

struct RewardsListResponse: Codable {
    let rewards: [RewardDTO]
    let lastUpdated: Date
}

struct ClaimRewardRequest: Codable {
    let rewardId: String
    let userId: String
    let timestamp: Date
    let nonce: String
}

struct ClaimRewardResponse: Codable {
    let transactionId: String
    let pointsDeducted: Int
    let newBalance: Int
    let claimTimestamp: Date
}

struct ClaimResponse {
    let transactionId: String
    let pointsDeducted: Int
    let newBalance: Int
    let claimTimestamp: Date
}

struct RewardHistoryRequest: Codable {
    let userId: String
    let page: Int
    let pageSize: Int
}

struct RewardHistoryResponse {
    let claims: [ClaimedReward]
    let totalCount: Int
    let hasMorePages: Bool
    let currentPage: Int
}
```

**Key Service Features**:
- ✅ Comprehensive error handling and retry logic
- ✅ Advanced caching with TTL support
- ✅ Authentication and security integration
- ✅ Offline support with stale data fallback
- ✅ Modern async/await and completion handler APIs
- ✅ Analytics and monitoring integration
- ✅ Request signing and security measures
- ✅ Network reachability checking
- ✅ Exponential backoff retry strategy

---

## Implementation Best Practices

### Architecture Principles

#### Single Responsibility Principle
- **View**: Handle UI presentation and user interaction only
- **Interactor**: Contain business logic and data processing exclusively
- **Presenter**: Manage data transformation and view state coordination
- **Entity**: Represent pure data models with validation logic
- **Router**: Handle navigation and module coordination

#### Protocol-Oriented Design
```swift
// Use protocols for all component communications
protocol FeatureBusinessLogic: AnyObject {
    func executeBusinessOperation()
}

protocol FeaturePresentationLogic: AnyObject {
    func presentResults(_ data: BusinessData)
}

protocol FeatureDisplayLogic: AnyObject {
    func displayFormattedResults(_ viewModels: [ViewModel])
}
```

### Code Quality Standards

#### Dependency Injection
```swift
// Constructor injection for dependencies
init(
    networkService: NetworkServiceProtocol,
    cacheManager: CacheManagerProtocol,
    analyticsTracker: AnalyticsTracking
) {
    self.networkService = networkService
    self.cacheManager = cacheManager
    self.analyticsTracker = analyticsTracker
}
```

#### Error Handling Patterns
```swift
// Comprehensive error handling
enum FeatureError: Error {
    case networkError(underlying: Error)
    case validationError(message: String)
    case businessRuleViolation(rule: String)
    
    var userFriendlyMessage: String {
        // Return localized, user-friendly error messages
    }
}
```

#### Async Programming
```swift
// Support both modern async/await and completion handlers
func fetchData() async throws -> [DataModel] {
    return try await withCheckedThrowingContinuation { continuation in
        fetchData { result in
            continuation.resume(with: result)
        }
    }
}
```

### Testing Considerations

#### Testable Architecture
- Use dependency injection for all external dependencies
- Create protocol abstractions for mockable components
- Separate business logic from UI concerns
- Design for isolated unit testing

#### Mock Strategy
```swift
// Protocol-based mocking
protocol NetworkServiceProtocol {
    func fetchData(completion: @escaping (Result<Data, Error>) -> Void)
}

class MockNetworkService: NetworkServiceProtocol {
    var stubResult: Result<Data, Error>?
    
    func fetchData(completion: @escaping (Result<Data, Error>) -> Void) {
        if let result = stubResult {
            completion(result)
        }
    }
}
```

### Performance Guidelines

#### Memory Management
```swift
// Use weak references to prevent retain cycles
weak var presenter: FeaturePresentationLogic?

// Capture self weakly in closures
networkService.fetchData { [weak self] result in
    self?.handleResponse(result)
}
```

#### Threading Best Practices
```swift
// Perform network operations on background threads
DispatchQueue.global(qos: .userInitiated).async {
    // Heavy work here
    DispatchQueue.main.async {
        // UI updates on main thread
        self.presenter?.presentResults(data)
    }
}
```

### Security Recommendations

#### Data Protection
- Encrypt sensitive data in transit and at rest
- Implement certificate pinning for API communications
- Validate all input data and API responses
- Use secure storage for authentication tokens

#### Authentication Integration
```swift
// Secure authentication handling
private func executeAuthenticatedRequest<T>(
    endpoint: Endpoint,
    completion: @escaping (Result<T, Error>) -> Void
) {
    guard authenticationService.isAuthenticated else {
        completion(.failure(ServiceError.authenticationRequired))
        return
    }
    
    // Proceed with authenticated request
}
```

### Accessibility Integration

#### Inclusive Design
```swift
// Comprehensive accessibility support
struct ViewModel {
    let accessibilityLabel: String
    let accessibilityHint: String?
    let accessibilityTraits: UIAccessibilityTraits
    
    init(data: BusinessData) {
        self.accessibilityLabel = createAccessibilityLabel(for: data)
        self.accessibilityHint = createAccessibilityHint(for: data)
        self.accessibilityTraits = determineAccessibilityTraits(for: data)
    }
}
```

### Monitoring and Analytics

#### Comprehensive Tracking
```swift
// Analytics integration at component boundaries
func executeBusinessOperation() {
    analyticsTracker.track(
        event: "business_operation_started",
        parameters: ["operation_type": "data_fetch"]
    )
    
    // Business logic execution
    
    analyticsTracker.track(
        event: "business_operation_completed",
        parameters: [
            "operation_type": "data_fetch",
            "success": true,
            "duration": executionTime
        ]
    )
}
```

### Documentation Standards

#### Code Documentation
```swift
/// Comprehensive method documentation
/// - Parameters:
///   - userId: Unique identifier for the user
///   - options: Configuration options for the operation
/// - Returns: Processed business data or throws error
/// - Throws: `BusinessError` if validation fails or network error occurs
func processUserData(
    userId: String, 
    options: ProcessingOptions
) async throws -> ProcessedData {
    // Implementation
}
```

### Localization Support

#### Internationalization
```swift
// Proper localization integration
enum LocalizedStrings {
    enum Rewards {
        static let title = NSLocalizedString(
            "rewards.title",
            comment: "Title for rewards screen"
        )
        static let pointsFormat = NSLocalizedString(
            "rewards.points.format",
            comment: "Format string for displaying points"
        )
    }
}
```

These best practices ensure your VIPER implementation is maintainable, scalable, testable, and follows iOS development standards while providing excellent user experience and developer productivity. 