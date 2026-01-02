# iOS Debugging and Explanation Prompts

This document contains prompts for debugging and explaining iOS code issues using the VIPER architecture pattern.

## Table of Contents

1. [Code Explanation & Review](#code-explanation--review)
2. [Bug Diagnosis (No Output/UI Update)](#bug-diagnosis-no-outputui-update)
3. [Crash Log Interpretation](#crash-log-interpretation)
4. [Memory Leak Detection](#memory-leak-detection)
5. [Logic Error and Fix Suggestions](#logic-error-and-fix-suggestions)

---

## Code Explanation & Review

### Use Case
Use this prompt when a developer needs to understand a complex piece of code or suspect there's a bug. It asks the assistant to explain what the code is doing and highlight potential issues. This is useful for reviewing an unfamiliar Interactor or Presenter function to ensure it meets requirements.

### Scenario
Reviewing and understanding complex Swift code within VIPER components.

### Prompt
Explain the following Swift code snippet from the [FeatureName]Interactor/Presenter and identify any potential problems or bugs. Provide a clear, step-by-step explanation of the logic. If you notice anti-patterns or mistakes (such as improper optional handling, missed thread handling, or a misuse of VIPER boundaries), point them out and suggest improvements.

Code:
```swift
// (Insert the code snippet here)
```

### Example

**Code to Review**:
```swift
func processRewards() {
    let rewards = try! JSONDecoder().decode([Reward].self, from: data)
    for reward in rewards {
        updateUI(with: reward)
    }
}
```

**Explanation & Issues**:

**Step-by-step breakdown**:
1. Attempts to decode JSON data into an array of Reward objects
2. Iterates through each reward
3. Updates UI directly for each reward

**Potential Issues Identified**:

1. **Force Unwrapping**: `try!` will crash the app if JSON decoding fails
   ```swift
   // Fix: Use proper error handling
   do {
       let rewards = try JSONDecoder().decode([Reward].self, from: data)
       // Process rewards
   } catch {
       // Handle error appropriately
       presenter?.presentError(error.localizedDescription)
   }
   ```

2. **VIPER Boundary Violation**: Direct UI updates from Interactor
   ```swift
   // Fix: Send data to Presenter instead
   presenter?.presentRewards(rewards)
   ```

3. **Threading Issues**: No guarantee this runs on main thread
   ```swift
   // Fix: Ensure UI updates happen on main thread
   DispatchQueue.main.async {
       presenter?.presentRewards(rewards)
   }
   ```

**Improved Version**:
```swift
func processRewards() {
    do {
        let rewards = try JSONDecoder().decode([Reward].self, from: data)
        DispatchQueue.main.async { [weak self] in
            self?.presenter?.presentRewards(rewards)
        }
    } catch {
        DispatchQueue.main.async { [weak self] in
            self?.presenter?.presentError(error.localizedDescription)
        }
    }
}
```

---

## Bug Diagnosis (No Output/UI Update)

### Use Case
Use this prompt when a certain user action does not produce the expected result in the UI, and you suspect a disconnect in the VIPER flow. For example, tapping a button should refresh a list but nothing happens. The prompt guides debugging through the VIPER chain to find where the breakdown is (perhaps the Presenter's method isn't called, or the Interactor isn't returning data).

### Scenario
Diagnosing issues where user actions don't produce expected UI updates.

### Prompt
Given the scenario: **[describe the bug, e.g. "Tapping Save on the settings screen doesn't show the success message"]**, analyze the **[FeatureName]** module's flow to find the issue. Check the View (does it call the Presenter correctly on action?), the Presenter (does it call the Interactor and handle response?), and the Interactor (does it execute the logic and call back via its output?). Provide a diagnostic approach: which logs or breakpoints to use in each layer. Then suggest a likely cause (for instance, 'The Presenter's delegate to the Interactor was never set, so the call never reaches the Interactor' or 'The Interactor returns data but the Presenter's output method isn't invoking the view'). Finally, propose a fix once the issue is identified.

### Example

**Bug**: Tapping "Claim Reward" button doesn't show success message.

**Diagnostic Approach**:

1. **View Layer Check**:
   ```swift
   @IBAction func claimButtonTapped(_ sender: UIButton) {
       print("🔍 DEBUG: Claim button tapped")
       presenter?.didTapClaimReward(rewardId: currentReward.id)
   }
   ```
   **Breakpoint**: Set breakpoint on button action method
   **Verify**: Action method is called and presenter method is invoked

2. **Presenter Layer Check**:
   ```swift
   func didTapClaimReward(rewardId: String) {
       print("🔍 DEBUG: Presenter received claim request for: \(rewardId)")
       interactor?.claimReward(rewardId: rewardId)
   }
   ```
   **Breakpoint**: Set breakpoint in presenter method
   **Verify**: Method receives correct parameters and calls interactor

3. **Interactor Layer Check**:
   ```swift
   func claimReward(rewardId: String) {
       print("🔍 DEBUG: Interactor processing claim for: \(rewardId)")
       rewardService.claimReward(rewardId) { [weak self] result in
           print("🔍 DEBUG: Service returned: \(result)")
           switch result {
           case .success:
               self?.presenter?.presentClaimSuccess()
           case .failure(let error):
               self?.presenter?.presentClaimError(error.localizedDescription)
           }
       }
   }
   ```
   **Breakpoint**: Set breakpoint in interactor method and completion handler

**Common Issues & Fixes**:

1. **View-Presenter Not Wired**:
   ```swift
   // Issue: Presenter is nil
   // Fix: Ensure proper wiring in module builder
   view.presenter = presenter
   ```

2. **Presenter-Interactor Not Connected**:
   ```swift
   // Issue: Interactor not set
   // Fix: Wire in module setup
   presenter.interactor = interactor
   interactor.presenter = presenter
   ```

3. **Weak Reference Issues**:
   ```swift
   // Issue: Presenter deallocated
   // Fix: Ensure proper retention
   class ViewController {
       var presenter: RewardPresenter! // Strong reference
   }
   ```

4. **Threading Issues**:
   ```swift
   // Issue: UI update not on main thread
   // Fix: Dispatch to main queue
   DispatchQueue.main.async {
       self?.view?.showSuccessMessage()
   }
   ```

---

## Crash Log Interpretation

### Use Case
Use this prompt to decode a crash log or error message and tie it back to the code. In iOS, crash logs can be cryptic; this prompt helps interpret, for example, an exception or a fatal error in a VIPER module (maybe a force unwrap in an Entity, or an out-of-bounds in a Presenter's formatting). It explains the cause and suggests a fix.

### Scenario
Analyzing crash logs to identify root causes and implement fixes.

### Prompt
Analyze the following crash log and the related code in **[FeatureName]**. 

**Log excerpt:** 
```
[paste relevant parts of the stack trace or error message]
```

Explain what is causing the crash or error, referencing the functions or lines in the stack trace (e.g., a nil optional unwrapped in the Presenter, or an index out of range in the View). Then, suggest a solution to fix the issue (for instance, add nil checking in the Interactor's response handling, or adjust the logic to prevent the out-of-range access). Provide a clear explanation suitable for the team to understand the root cause and the fix.

### Example

**Crash Log**:
```
Thread 1: Fatal error: Unexpectedly found nil while unwrapping an Optional value

0   RewardsApp    0x000102834 RewardsDashboardPresenter.formatRewardTitle line 45
1   RewardsApp    0x000102856 RewardsDashboardPresenter.presentRewards line 32
2   RewardsApp    0x000102901 RewardsDashboardInteractor.fetchRewards line 28
```

**Code at Crash Location**:
```swift
// Line 45 in RewardsDashboardPresenter.formatRewardTitle
func formatRewardTitle(_ reward: Reward) -> String {
    return reward.title! // ⚠️ CRASH HERE
}
```

**Root Cause Analysis**:

The crash occurs because `reward.title` is an optional property that contains `nil`, but the code force-unwraps it with `!`. This happens when:
1. Server returns reward data with missing title field
2. JSON parsing succeeds but title field is null
3. Presenter assumes title will always exist

**Stack Trace Explanation**:
1. `fetchRewards` in Interactor receives data from service
2. `presentRewards` in Presenter processes the reward array
3. `formatRewardTitle` attempts to force-unwrap nil title → **CRASH**

**Fixes**:

1. **Safe Unwrapping**:
   ```swift
   func formatRewardTitle(_ reward: Reward) -> String {
       return reward.title ?? "Unknown Reward"
   }
   ```

2. **Guard Statement**:
   ```swift
   func formatRewardTitle(_ reward: Reward) -> String {
       guard let title = reward.title else {
           return "Unknown Reward"
       }
       return title
   }
   ```

3. **Model Validation**:
   ```swift
   // In Interactor, validate data before sending to Presenter
   let validRewards = rewards.filter { $0.title != nil }
   presenter?.presentRewards(validRewards)
   ```

4. **Better JSON Parsing**:
   ```swift
   struct Reward: Codable {
       let id: String
       let title: String // Non-optional with default
       let points: Int
       
       init(from decoder: Decoder) throws {
           let container = try decoder.container(keyedBy: CodingKeys.self)
           id = try container.decode(String.self, forKey: .id)
           title = try container.decodeIfPresent(String.self, forKey: .title) ?? "Unknown"
           points = try container.decode(Int.self, forKey: .points)
       }
   }
   ```

---

## Memory Leak Detection

### Use Case
Investigate a potential memory leak in a VIPER module. After closing a screen, some objects (e.g. Presenter or ViewController) are not deallocated. This helps maintain app performance and is crucial for features that the user navigates in and out of frequently.

### Scenario
Identifying and fixing memory leaks in VIPER modules.

### Prompt
Investigate a potential memory leak in the **[FeatureName]** module. After closing the **[FeatureName]** screen, some objects (e.g. Presenter or ViewController) are not deallocated. Walk through the code to identify strong reference cycles or other memory management issues. Check things like: the Presenter-View relationship (is the view holding a strong reference to the Presenter or vice-versa where it should be weak?), any closures or DispatchWorkItem in the Interactor that capture `self` strongly, singletons or Notification observers not removed, etc. Provide an explanation of any problematic code you find and recommend how to fix it (for example, mark a delegate property as `weak`, or remove observers in `deinit`). The output should detail each step of the investigation and the resolution.

### Example

**Memory Leak Investigation**:

**Step 1: Check Reference Cycles**

**Problem Code**:
```swift
class RewardsDashboardPresenter {
    var view: RewardsDashboardDisplayLogic // ⚠️ Strong reference
    var interactor: RewardsDashboardBusinessLogic
}

class RewardsDashboardViewController: UIViewController {
    var presenter: RewardsDashboardPresenter! // Strong reference
}
```

**Issue**: Presenter holds strong reference to View, View holds strong reference to Presenter → Retain Cycle

**Fix**:
```swift
class RewardsDashboardPresenter {
    weak var view: RewardsDashboardDisplayLogic? // ✅ Weak reference
    var interactor: RewardsDashboardBusinessLogic
}
```

**Step 2: Check Closure Captures**

**Problem Code**:
```swift
func fetchRewards() {
    rewardService.getRewards { result in
        self.presenter?.presentRewards(result) // ⚠️ Strong capture of self
    }
}
```

**Fix**:
```swift
func fetchRewards() {
    rewardService.getRewards { [weak self] result in
        self?.presenter?.presentRewards(result) // ✅ Weak capture
    }
}
```

**Step 3: Check Notification Observers**

**Problem Code**:
```swift
class RewardsDashboardViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        NotificationCenter.default.addObserver(
            self,
            selector: #selector(handleRewardUpdate),
            name: .rewardUpdated,
            object: nil
        )
        // ⚠️ Observer never removed
    }
}
```

**Fix**:
```swift
class RewardsDashboardViewController {
    deinit {
        NotificationCenter.default.removeObserver(self) // ✅ Clean up
    }
    
    // Or use modern block-based API with automatic cleanup
    private var rewardObserver: NSObjectProtocol?
    
    override func viewDidLoad() {
        super.viewDidLoad()
        rewardObserver = NotificationCenter.default.addObserver(
            forName: .rewardUpdated,
            object: nil,
            queue: .main
        ) { [weak self] _ in
            self?.handleRewardUpdate()
        }
    }
    
    deinit {
        if let observer = rewardObserver {
            NotificationCenter.default.removeObserver(observer)
        }
    }
}
```

**Step 4: Check Timer/Dispatch Sources**

**Problem Code**:
```swift
class RewardsDashboardInteractor {
    private var timer: Timer?
    
    func startPeriodicUpdates() {
        timer = Timer.scheduledTimer(withTimeInterval: 30) { _ in
            self.fetchRewards() // ⚠️ Strong capture in timer
        }
    }
}
```

**Fix**:
```swift
class RewardsDashboardInteractor {
    private var timer: Timer?
    
    func startPeriodicUpdates() {
        timer = Timer.scheduledTimer(withTimeInterval: 30) { [weak self] _ in
            self?.fetchRewards() // ✅ Weak capture
        }
    }
    
    deinit {
        timer?.invalidate() // ✅ Clean up timer
    }
}
```

**Memory Leak Detection Tools**:

1. **Instruments Leaks Tool**: Use to detect actual leaks
2. **Debug Memory Graph**: Xcode → Debug → View Memory Graph Hierarchy
3. **Deinit Logging**: Add logging to verify deallocation
   ```swift
   deinit {
       print("✅ \(String(describing: type(of: self))) deallocated")
   }
   ```

---

## Logic Error and Fix Suggestions

### Use Case
Debug a logical error where the code runs without crashing but produces incorrect results. For instance, an order total is calculated wrong or a user preference isn't saved. It asks for tracing through the relevant VIPER components to find where the logic deviates from expectations, then suggests corrections.

### Scenario
Identifying and fixing logical errors in business logic implementation.

### Prompt
A logical issue has been reported in **[FeatureName]**: **[describe the issue, e.g. "Discount is applied incorrectly in the final price" or "Notification preference changes are not reflected"]**. Debug this problem by inspecting the code path across the module. Start from where the input enters the system (e.g. the View or Presenter method handling user input) and follow through the Interactor's processing to the output. Identify where the actual behavior diverges from the expected behavior. For example, maybe a wrong conditional in the Interactor, or the Presenter not handling a certain response. Once identified, describe how to fix the logic – such as adjusting an algorithm, correcting the conditional logic, or updating the sequence of calls. Provide a clear explanation of both the bug and the fix, so the team can understand the change.

### Example

**Issue**: Reward discount not applied correctly - users with 500+ points should get 10% discount, but they're getting 0% discount.

**Code Investigation**:

**View Layer** (Entry Point):
```swift
@IBAction func applyDiscountTapped(_ sender: UIButton) {
    presenter?.calculateDiscountedPrice(for: currentReward, userPoints: userPoints)
}
```
✅ **Status**: View correctly passes user points to presenter

**Presenter Layer**:
```swift
func calculateDiscountedPrice(for reward: Reward, userPoints: Int) {
    interactor?.calculateDiscount(reward: reward, userPoints: userPoints)
}
```
✅ **Status**: Presenter correctly forwards request to interactor

**Interactor Layer** (Business Logic):
```swift
func calculateDiscount(reward: Reward, userPoints: Int) {
    var discountPercentage = 0
    
    // ⚠️ BUG: Wrong condition
    if userPoints > 1000 {  // Should be 500, not 1000
        discountPercentage = 10
    } else {
        discountPercentage = 0
    }
    
    let discountedPrice = reward.price * (100 - discountPercentage) / 100
    presenter?.presentDiscountedPrice(discountedPrice, discount: discountPercentage)
}
```

**Root Cause**: 
- **Expected**: Users with 500+ points get 10% discount
- **Actual**: Only users with 1000+ points get discount
- **Issue**: Incorrect threshold in conditional statement

**Fix**:
```swift
func calculateDiscount(reward: Reward, userPoints: Int) {
    var discountPercentage = 0
    
    // ✅ Fixed: Correct threshold
    if userPoints >= 500 {  // Changed from 1000 to 500
        discountPercentage = 10
    } else {
        discountPercentage = 0
    }
    
    let discountedPrice = reward.price * (100 - discountPercentage) / 100
    presenter?.presentDiscountedPrice(discountedPrice, discount: discountPercentage)
}
```

**Additional Improvements**:

1. **Make Logic More Readable**:
   ```swift
   func calculateDiscount(reward: Reward, userPoints: Int) {
       let discountPercentage = userPoints >= 500 ? 10 : 0
       let discountedPrice = reward.price * (100 - discountPercentage) / 100
       presenter?.presentDiscountedPrice(discountedPrice, discount: discountPercentage)
   }
   ```

2. **Extract Constants**:
   ```swift
   private enum DiscountRules {
       static let minimumPointsForDiscount = 500
       static let discountPercentage = 10
   }
   
   func calculateDiscount(reward: Reward, userPoints: Int) {
       let discountPercentage = userPoints >= DiscountRules.minimumPointsForDiscount 
           ? DiscountRules.discountPercentage 
           : 0
       let discountedPrice = reward.price * (100 - discountPercentage) / 100
       presenter?.presentDiscountedPrice(discountedPrice, discount: discountPercentage)
   }
   ```

3. **Add Unit Tests** to prevent regression:
   ```swift
   func testDiscountCalculation() {
       // Test case 1: User with 500 points gets discount
       interactor.calculateDiscount(reward: reward, userPoints: 500)
       XCTAssertEqual(mockPresenter.lastDiscountPercentage, 10)
       
       // Test case 2: User with 499 points gets no discount  
       interactor.calculateDiscount(reward: reward, userPoints: 499)
       XCTAssertEqual(mockPresenter.lastDiscountPercentage, 0)
   }
   ```

---

## Debugging Best Practices

### General Debugging Workflow
1. **Reproduce the Issue**: Ensure you can consistently recreate the problem
2. **Isolate the Component**: Identify which VIPER layer is involved
3. **Add Logging**: Use strategic print statements or logging frameworks
4. **Use Breakpoints**: Step through code execution
5. **Check Assumptions**: Verify data at each step
6. **Test the Fix**: Ensure the solution works and doesn't break other functionality

### VIPER-Specific Debugging
- **View**: Check if user actions trigger presenter methods
- **Presenter**: Verify data transformation and view updates
- **Interactor**: Validate business logic and service calls
- **Entity**: Ensure data models work correctly
- **Router**: Confirm navigation logic

### Tools and Techniques
- **Xcode Debugger**: Breakpoints, variable inspection, call stack
- **Instruments**: Memory leaks, performance profiling
- **Debug Memory Graph**: Visual representation of object relationships
- **Logging**: Strategic logging at component boundaries
- **Unit Tests**: Test individual components in isolation 