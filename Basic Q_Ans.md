## 1. Basic iOS Questions

### Q1: What is the difference between frame and bounds?
**Answer:**
- **Frame**: Position and size of a view relative to its superview's coordinate system
- **Bounds**: Position and size of a view relative to its own coordinate system
- Frame changes when you move/resize the view, bounds typically has origin (0,0)

### Q2: Explain the iOS App Lifecycle
**Answer:**
1. **Not Running**: App hasn't been launched
2. **Inactive**: App is running but not receiving events
3. **Active**: App is running and receiving events
4. **Background**: App is executing code but not visible
5. **Suspended**: App is in background but not executing code

### Q3: What is ARC (Automatic Reference Counting)?
**Answer:**
- Memory management system that automatically manages retain/release cycles
- Prevents memory leaks by automatically inserting retain/release calls
- Works at compile time, not runtime
- Handles strong, weak, and unowned references

### Q4: Difference between strong, weak, and unowned references?
**Answer:**
- **Strong**: Default, keeps object in memory, increases reference count
- **Weak**: Doesn't increase reference count, becomes nil when object is deallocated
- **Unowned**: Doesn't increase reference count, doesn't become nil (crashes if accessed after deallocation)

---

## 2. Intermediate iOS Questions

### Q5: What is a delegate pattern and how is it implemented?
**Answer:**
```swift
protocol CustomDelegate: AnyObject {
    func didFinishTask()
}

class MyClass {
    weak var delegate: CustomDelegate?
    
    func performTask() {
        // Do work
        delegate?.didFinishTask()
    }
}
```

### Q6: Explain closures and their capture behavior
**Answer:**
- Closures are self-contained blocks of functionality
- They capture and store references to variables from surrounding context
- Can cause retain cycles if not handled properly with `[weak self]` or `[unowned self]`

### Q7: What is the difference between synchronous and asynchronous operations?
**Answer:**
- **Synchronous**: Blocks the current thread until operation completes
- **Asynchronous**: Doesn't block, operation runs on different thread
- Use GCD (Grand Central Dispatch) or async/await for async operations

### Q8: Explain MVC, MVP, and MVVM patterns
**Answer:**
- **MVC**: Model-View-Controller (Apple's default)
- **MVP**: Model-View-Presenter (View is passive)
- **MVVM**: Model-View-ViewModel (Uses data binding, popular with SwiftUI)

---

## 3. Advanced iOS Questions

### Q9: How do you handle memory leaks in iOS?
**Answer:**
1. Use Instruments (Leaks, Allocations)
2. Avoid retain cycles with weak/unowned references
3. Use `[weak self]` in closures
4. Properly manage delegates (weak references)
5. Unsubscribe from notifications in deinit

### Q10: Explain Core Data and its components
**Answer:**
- **NSManagedObjectContext**: Scratchpad for working with managed objects
- **NSManagedObjectModel**: Schema describing entities
- **NSPersistentStoreCoordinator**: Manages persistent stores
- **NSManagedObject**: Objects managed by Core Data

### Q11: What is Grand Central Dispatch (GCD)?
**Answer:**
```swift
// Main queue
DispatchQueue.main.async {
    // UI updates
}

// Background queue
DispatchQueue.global(qos: .background).async {
    // Heavy computation
}

// Custom queue
let customQueue = DispatchQueue(label: "com.company.queue")
```

### Q12: Explain different types of notifications in iOS
**Answer:**
1. **Local Notifications**: Scheduled by app, delivered by system
2. **Remote (Push) Notifications**: Sent from server via APNs
3. **NSNotificationCenter**: For in-app communication between objects

---

## 4. SwiftUI Questions (Modern iOS Development)

### Q13: What are the main differences between UIKit and SwiftUI?
**Answer:**
- **UIKit**: Imperative, mature, more control, larger codebase
- **SwiftUI**: Declarative, modern, less code, automatic updates with state changes

### Q14: Explain @State, @Binding, and @ObservedObject in SwiftUI
**Answer:**
- **@State**: For simple value types owned by the view
- **@Binding**: Creates two-way connection to @State property
- **@ObservedObject**: For reference types conforming to ObservableObject

---

## 5. Networking Questions

### Q15: How do you make network requests in iOS?
**Answer:**
```swift
// URLSession approach
let url = URL(string: "https://api.example.com/data")!
let task = URLSession.shared.dataTask(with: url) { data, response, error in
    // Handle response
}
task.resume()

// Async/await approach (iOS 15+)
let (data, response) = try await URLSession.shared.data(from: url)
```

### Q16: How do you handle JSON parsing in Swift?
**Answer:**
```swift
struct User: Codable {
    let id: Int
    let name: String
}

// Decode JSON
let user = try JSONDecoder().decode(User.self, from: jsonData)

// Encode to JSON
let jsonData = try JSONEncoder().encode(user)
```

---

## 6. Performance Questions

### Q17: How do you optimize table view performance?
**Answer:**
1. Use cell reuse with `dequeueReusableCell`
2. Avoid complex layouts in cells
3. Use lazy loading for images
4. Implement proper caching
5. Use `prepareForReuse()` to reset cell state

### Q18: What is lazy loading and when would you use it?
**Answer:**
- Delayed initialization of expensive resources
- Use for images, large data sets, heavy computations
- Improves app startup time and memory usage

---

## 7. Security Questions

### Q19: How do you store sensitive data securely in iOS?
**Answer:**
1. **Keychain**: For passwords, tokens, certificates
2. **Core Data with encryption**: For larger datasets
3. **Never use UserDefaults** for sensitive data
4. Use **App Transport Security (ATS)** for network calls

### Q20: What is App Transport Security (ATS)?
**Answer:**
- Security feature that enforces secure connections
- Requires HTTPS for network calls
- Can be configured in Info.plist
- Prevents man-in-the-middle attacks

---

## 8. Testing Questions

### Q21: What types of testing do you implement in iOS?
**Answer:**
1. **Unit Tests**: Test individual components (XCTest)
2. **Integration Tests**: Test component interactions
3. **UI Tests**: Test user interface (XCUITest)
4. **Performance Tests**: Measure execution time

### Q22: How do you write a unit test in iOS?
**Answer:**
```swift
import XCTest
@testable import MyApp

class MyAppTests: XCTestCase {
    func testUserCreation() {
        let user = User(name: "John", age: 25)
        XCTAssertEqual(user.name, "John")
        XCTAssertEqual(user.age, 25)
    }
}
```

---

## 9. Project-Based Questions (Common in LTI Mindtree)

### Q23: Walk me through your most challenging iOS project
**Preparation Tips:**
- Explain the problem you solved
- Discuss architecture decisions
- Mention technologies used
- Highlight challenges faced and solutions implemented
- Quantify the impact (performance improvements, user engagement, etc.)

### Q24: How did you handle offline functionality in your app?
**Answer:**
1. **Core Data** for local storage
2. **Network reachability** detection
3. **Sync mechanisms** when connectivity returns
4. **User feedback** for offline status
5. **Conflict resolution** for data synchronization

### Q25: Describe how you implemented push notifications
**Answer:**
1. Configure APNs certificates
2. Register for remote notifications
3. Handle notification permissions
4. Process notification payloads
5. Update UI based on notification content

---

## 10. Coding Questions (Live Coding Round)

### Q26: Reverse a string in Swift
```swift
func reverseString(_ str: String) -> String {
    return String(str.reversed())
}

// Alternative approach
func reverseStringManual(_ str: String) -> String {
    var reversed = ""
    for char in str {
        reversed = String(char) + reversed
    }
    return reversed
}
```

### Q27: Find duplicate elements in an array
```swift
func findDuplicates<T: Hashable>(_ array: [T]) -> [T] {
    var seen = Set<T>()
    var duplicates = Set<T>()
    
    for element in array {
        if seen.contains(element) {
            duplicates.insert(element)
        } else {
            seen.insert(element)
        }
    }
    
    return Array(duplicates)
}
```
