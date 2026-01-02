# iOS Unit Test Generation Prompts

This document contains prompts for generating comprehensive unit tests for iOS applications using the VIPER architecture pattern.

## Table of Contents

1. [Interactor Unit Tests (XCTest/Quick)](#interactor-unit-tests-xctestquick)
2. [Presenter Unit Tests and Mocking](#presenter-unit-tests-and-mocking)
3. [End-to-End Use Case Test](#end-to-end-use-case-test)
4. [Data Model (Entity) Tests](#data-model-entity-tests)
5. [Async Operation Tests (Using Expectations)](#async-operation-tests-using-expectations)

---

## Interactor Unit Tests (XCTest/Quick)

### Use Case
Use this prompt to create unit tests for Interactor logic. Interactors contain core business rules and, being UI-independent, are straightforward to test. This prompt can be applied to any feature's Interactor (e.g. testing that an OrderInteractor correctly calculates order totals, or that a PreferencesInteractor correctly filters preferences). The prompt encourages using either XCTest or Quick/Nimble for clear, behavior-driven test descriptions.

### Scenario
Testing business logic within Interactor components.

### Prompt
Write unit tests for [FeatureName]Interactor's [functionName] behavior. Include test cases for the main success scenario and edge cases (e.g. error or no data scenarios). Use XCTest or Quick/Nimble for the test style – for example, you can write BDD-style specs with Quick (describe/context/it) and expectations with Nimble. Ensure each test clearly states the given conditions, when the interactor method is invoked, and then the expected outcome (Given-When-Then). The tests should verify that the Interactor: (a) calls the appropriate data source (or RemoteService) when needed (you can inject a stub data service if using Quick/Nimble), and (b) produces the correct result or calls the Presenter output with the right data. Provide the test code with any necessary setup and tear-down.

### Example

**Test for RewardsDashboardInteractor.fetchRewards() success scenario**:

```swift
func testFetchRewards_success() {
    // Given
    let mockService = MockRewardService()
    mockService.stubResult = .success([Reward(id: "1", title: "Free Coffee", points: 100)])
    let mockPresenter = MockRewardsDashboardPresenter()
    let interactor = RewardsDashboardInteractor(service: mockService)
    interactor.presenter = mockPresenter
    
    // When
    interactor.fetchRewards()
    
    // Then
    expect(mockPresenter.receivedRewards).toNot(beNil())
    expect(mockPresenter.receivedRewards?.count).to(equal(1))
    expect(mockPresenter.receivedRewards?.first?.title).to(equal("Free Coffee"))
}

func testFetchRewards_failure() {
    // Given
    let mockService = MockRewardService()
    mockService.stubResult = .failure(NetworkError.connectionFailed)
    let mockPresenter = MockRewardsDashboardPresenter()
    let interactor = RewardsDashboardInteractor(service: mockService)
    interactor.presenter = mockPresenter
    
    // When
    interactor.fetchRewards()
    
    // Then
    expect(mockPresenter.receivedError).toNot(beNil())
    expect(mockPresenter.receivedError).to(contain("connection"))
}
```

---

## Presenter Unit Tests and Mocking

### Use Case
Use this prompt to generate tests for Presenter logic, including how it handles data from the Interactor and updates the View. It's common to use a mock View to verify the Presenter's outputs (for example, that a showError(message:) is called on the view when the interactor returns an error). This prompt ensures the Presenter's formatting and decision logic is fully tested.

### Scenario
Testing presentation logic and view updates in Presenter components.

### Prompt
Create unit tests for [FeatureName]Presenter. Focus on a scenario where [FeatureName]Interactor returns data or an error, and verify that the Presenter responds correctly. Use a mock View (conforming to the Presenter's view interface) to assert that the Presenter calls the right methods on the View. For instance, test that when the interactor provides a valid [Entity] list, the Presenter transforms it into view models and invokes display[Entity]List(...) on the view with expected values. Likewise, test the error path (have the interactor output an error or empty result and verify the Presenter calls an error display method). Use Nimble's matchers for readable assertions (e.g. expect(mockView.lastMessage).to(equal("Network error")) for an error case). The test code should be written in Swift, using either Quick/Nimble or XCTest assertions, and demonstrate how to inject the mock view and interactor into the Presenter.

### Example

**Test for RewardsDashboardPresenter data transformation**:

```swift
class MockRewardsDashboardView: RewardsDashboardDisplayLogic {
    var displayedViewModels: [RewardItemViewModel] = []
    var lastErrorMessage: String?
    
    func displayRewards(_ viewModels: [RewardItemViewModel]) {
        displayedViewModels = viewModels
    }
    
    func displayError(_ message: String) {
        lastErrorMessage = message
    }
}

func testPresenterTransformsRewardsToViewModels() {
    // Given
    let mockView = MockRewardsDashboardView()
    let presenter = RewardsDashboardPresenter()
    presenter.view = mockView
    
    let rewards = [Reward(id: "1", title: "Coffee", points: 100)]
    
    // When
    presenter.presentRewards(rewards)
    
    // Then
    expect(mockView.displayedViewModels.count).to(equal(1))
    expect(mockView.displayedViewModels.first?.title).to(equal("Coffee"))
    expect(mockView.displayedViewModels.first?.pointsLabel).to(equal("100 pts"))
}

func testPresenterHandlesError() {
    // Given
    let mockView = MockRewardsDashboardView()
    let presenter = RewardsDashboardPresenter()
    presenter.view = mockView
    
    // When
    presenter.presentError("Network connection failed")
    
    // Then
    expect(mockView.lastErrorMessage).to(equal("Network connection failed"))
}
```

---

## End-to-End Use Case Test

### Use Case
Use this prompt to outline tests that cover the interaction between VIPER components for one use case, albeit still at the unit test level by using stubs or spies. For example, testing that when a view triggers an action, the Presenter invokes the Interactor, and subsequently the Presenter updates the view. This ensures the wiring of VIPER is correct.

### Scenario
Testing complete flow through VIPER components for a specific use case.

### Prompt
Write a comprehensive unit test for the [FeatureName] module's main use case, covering the flow from Presenter to Interactor to Presenter (and Presenter to View). Simulate a user action by calling the Presenter's [inputMethod] (from the View layer). Use a stub or spy for [FeatureName]Interactor that, when called by the Presenter, returns a predefined result (via its output protocol). Then assert that the Presenter, upon receiving this result, calls the correct method on the mock View with expected data. Essentially, this test will verify that the Presenter -> Interactor -> Presenter -> View flow is working: the Presenter forwards the request, the Interactor's response is handled, and the View is updated. Use Quick's describe/it blocks or XCTest functions to structure the test, and Nimble or XCTAssert to validate interactions (for example, a spy Interactor could set a flag that it was called, and the mock View captures the data presented). Provide the test code and briefly explain how it confirms the VIPER module integration logic.

### Example

**End-to-end test for viewDidLoad triggering fetch and updating view**:

```swift
class SpyRewardsInteractor: RewardsDashboardBusinessLogic {
    var fetchCalled = false
    var presenter: RewardsDashboardPresentationLogic?
    
    func fetchRewards() {
        fetchCalled = true
        // Simulate successful response
        let rewards = [Reward(id: "1", title: "Coffee", points: 100)]
        presenter?.presentRewards(rewards)
    }
}

func testViewDidLoadTriggersFlowAndUpdatesView() {
    // Given
    let mockView = MockRewardsDashboardView()
    let spyInteractor = SpyRewardsInteractor()
    let presenter = RewardsDashboardPresenter()
    
    // Wire up the components
    presenter.view = mockView
    presenter.interactor = spyInteractor
    spyInteractor.presenter = presenter
    
    // When
    presenter.viewDidLoad()
    
    // Then
    expect(spyInteractor.fetchCalled).to(beTrue())
    expect(mockView.displayedViewModels.count).to(equal(1))
    expect(mockView.displayedViewModels.first?.title).to(equal("Coffee"))
}
```

**Explanation**: This test confirms that the VIPER wiring is correct by verifying:
1. View action triggers Presenter method
2. Presenter calls Interactor
3. Interactor processes and calls back to Presenter
4. Presenter updates View with formatted data

---

## Data Model (Entity) Tests

### Use Case
Use this prompt to generate tests for model or entity transformations, such as JSON parsing or value computations. If a feature has an Entity (e.g. a UserPreference model with computed properties or a custom initializer), those can be unit tested to ensure correctness. This prompt ensures even the basic building blocks of the VIPER module have coverage.

### Scenario
Testing data models, JSON parsing, and computed properties in Entity objects.

### Prompt
Generate unit tests for the [FeatureName] module's Entity/model logic. For instance, if [EntityName] is a model that can be initialized from JSON or has computed properties, write tests to validate these. Provide sample JSON data and test that the model's initializer or Codable implementation correctly parses all fields (using dummy JSON strings or dictionaries). If the model has business rules (e.g. a computed property isValid or a method calculateDiscount()), write test cases for those as well. Use XCTAssert or Nimble expect to compare expected values (for example, ensure that an order total calculation returns the correct sum given test inputs). These tests should be small and focused on the Entity layer, independent of UI, running under XCTest or Quick as needed.

### Example

**Test for Reward entity JSON decoding**:

```swift
func testRewardDecoding() {
    // Given
    let json = """
    {
        "id": "1",
        "title": "Free Tea",
        "points": 50,
        "description": "Enjoy a complimentary tea"
    }
    """.data(using: .utf8)!
    
    // When
    let reward = try! JSONDecoder().decode(Reward.self, from: json)
    
    // Then
    XCTAssertEqual(reward.id, "1")
    XCTAssertEqual(reward.title, "Free Tea")
    XCTAssertEqual(reward.points, 50)
    XCTAssertEqual(reward.description, "Enjoy a complimentary tea")
}

func testRewardComputedProperties() {
    // Given
    let reward = Reward(id: "1", title: "Premium Coffee", points: 150)
    
    // When & Then
    XCTAssertTrue(reward.isPremium) // points > 100
    XCTAssertEqual(reward.displayText, "Premium Coffee (150 pts)")
}

func testRewardValidation() {
    // Given
    let validReward = Reward(id: "1", title: "Coffee", points: 50)
    let invalidReward = Reward(id: "", title: "", points: -10)
    
    // When & Then
    XCTAssertTrue(validReward.isValid)
    XCTAssertFalse(invalidReward.isValid)
}
```

---

## Async Operation Tests (Using Expectations)

### Use Case
Use this prompt for writing tests around asynchronous code, such as a RemoteService call or any completion handler logic in the Interactor. It emphasizes using XCTest expectations or Quick/Nimble's waiting utilities to properly handle async. This is important in features like Order Management where the Interactor might fetch data from an API asynchronously.

### Scenario
Testing asynchronous operations with proper expectation handling.

### Prompt
Write a unit test for an asynchronous operation in [FeatureName]Interactor using XCTest expectations (or Quick/Nimble's waitUntil if using Quick). For example, test the fetch[Data] function which calls the RemoteService. Use a stub RemoteService that invokes its completion after a short delay. In the test, call the interactor's method, then wait for the async callback. Assert that the interactor's completion delivers the expected result (e.g. an array of [Entity] or a specific error). If using XCTest, utilize expectation(description:) and waitForExpectations(timeout:) to wait for the result. If using Nimble, use waitUntil to achieve the same. The test should fail if the callback isn't called or returns an unexpected result. Provide the test implementation and ensure it's reliable (for instance, no flakiness by using an adequate timeout and calling fulfill on the expectation in the stub's completion).

### Example

**Test for async reward fetching with XCTest expectations**:

```swift
func testAsyncRewardFetch() {
    // Given
    let expectation = self.expectation(description: "Async fetch completes")
    let mockService = MockRewardService()
    let rewards = [
        Reward(id: "1", title: "Coffee", points: 100),
        Reward(id: "2", title: "Tea", points: 50)
    ]
    mockService.stubResult = .success(rewards)
    
    let interactor = RewardsDashboardInteractor(service: mockService)
    var receivedRewards: [Reward]?
    
    // When
    interactor.fetchRewards { result in
        switch result {
        case .success(let rewards):
            receivedRewards = rewards
        case .failure:
            XCTFail("Expected success but got failure")
        }
        expectation.fulfill()
    }
    
    // Then
    waitForExpectations(timeout: 2.0) { error in
        XCTAssertNil(error)
        XCTAssertEqual(receivedRewards?.count, 2)
        XCTAssertEqual(receivedRewards?.first?.title, "Coffee")
    }
}

// Using Quick/Nimble alternative
func testAsyncRewardFetchWithNimble() {
    // Given
    let mockService = MockRewardService()
    let interactor = RewardsDashboardInteractor(service: mockService)
    var result: Result<[Reward], Error>?
    
    // When
    interactor.fetchRewards { asyncResult in
        result = asyncResult
    }
    
    // Then
    waitUntil(timeout: .seconds(2)) { done in
        if result != nil {
            done()
        }
    }
    
    expect(result).toNot(beNil())
    switch result! {
    case .success(let rewards):
        expect(rewards.count).to(equal(2))
    case .failure:
        fail("Expected success")
    }
}
```

---

## Testing Best Practices

### General Guidelines
- **Arrange-Act-Assert**: Structure tests with clear Given-When-Then sections
- **Test Names**: Use descriptive names that explain the scenario
- **Mock Dependencies**: Use mocks/stubs for external dependencies
- **Fast Tests**: Keep tests fast and independent
- **Coverage**: Aim for high test coverage, especially for business logic

### VIPER-Specific Testing
- **Interactor**: Focus on business logic and data processing
- **Presenter**: Test data transformation and view updates
- **Entity**: Validate model behavior and JSON parsing
- **Router**: Test navigation logic (if complex)
- **Integration**: Test component interactions

### Async Testing Tips
- **Timeouts**: Use reasonable timeouts (2-5 seconds typically)
- **Expectations**: Always fulfill expectations to prevent hanging tests
- **Error Handling**: Test both success and failure scenarios
- **Threading**: Ensure callbacks happen on expected queues

### Mock Strategy
- **Protocols**: Use protocol-based mocking for flexibility
- **Spies**: Track method calls and parameters
- **Stubs**: Return predefined values for testing
- **Verification**: Assert interactions happened as expected 