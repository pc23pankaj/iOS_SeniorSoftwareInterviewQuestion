## 🧵 Swift Concurrency: `async`, `await`, `Actor`, `MainActor`

Swift’s concurrency model (introduced in **Swift 5.5**) is designed to safely and efficiently handle **asynchronous operations** and **multithreading**, replacing older patterns like closures, `DispatchQueue`, and `completionHandlers`.

---

### ✅ `async` — Declares an Asynchronous Function

* `async` marks a function that **can pause** its execution and **resume later**.
* It allows non-blocking operations to look synchronous.

```swift
func fetchUserProfile() async -> String {
    return "User loaded"
}
```

---

### ✅ `await` — Waits for an Async Function to Complete

* `await` is used to **suspend execution** until an `async` function returns a result.
* Must be used **inside an async context**.

```swift
func loadData() async {
    let result = await fetchUserProfile()
    print(result)
}
```

---

## 👤 `actor` — Safe Shared-State Container

* An `actor` is a **reference type** that protects its internal state by allowing **only one task to access it at a time**.
* Prevents **data races** in concurrent environments.

```swift
actor Counter {
    private var value = 0

    func increment() {
        value += 1
    }

    func getValue() -> Int {
        return value
    }
}
```

**Usage:**

```swift
let counter = Counter()
await counter.increment()
let val = await counter.getValue()
```

---

## 🎭 `@MainActor` — Ensures Main Thread Execution

* `@MainActor` guarantees that a function or property **runs on the main thread**.
* Essential for **UI updates**, as UI must be manipulated on the main thread.

### 💡 Use Cases:

* Updating SwiftUI or UIKit views
* Reading/writing view-related state in ViewModels

```swift
@MainActor
class ViewModel {
    var title = "Hello"

    func updateUI() {
        // Always runs on main thread
        print(title)
    }
}
```

You can also isolate specific methods:

```swift
@MainActor func showMessage() {
    print("On main thread")
}
```

Or switch context manually:

```swift
await MainActor.run {
    label.text = "Updated safely"
}
```

---

## ⚔️ `MainActor` vs `Actor` — Key Differences

| Feature                | `MainActor`                                 | `Actor`                                 |
| ---------------------- | ------------------------------------------- | --------------------------------------- |
| Purpose                | Ensures execution on the **main/UI thread** | Protects mutable state from data races  |
| Runs On                | Main thread                                 | Internal serial queue (not main thread) |
| Used For               | UI updates, ViewModels                      | Background state, data models           |
| Thread Safety          | Yes (UI-safe by default)                    | Yes (automatic locking)                 |
| Customizable Context?  | No (always main thread)                     | Yes (runs on its own context)           |
| Accessed With `await`? | Yes                                         | Yes                                     |

---

## ✅ Real-World Example: Combine Them

```swift
actor DataStore {
    private var value = 0

    func increment() {
        value += 1
    }

    func getValue() -> Int {
        return value
    }
}

@MainActor
class ViewModel: ObservableObject {
    @Published var displayValue: Int = 0
    let store = DataStore()

    func load() async {
        await store.increment()
        let value = await store.getValue()
        displayValue = value // Safe, because it's on MainActor
    }
}
```

---

## 🧠 Summary

| Concept      | Purpose                              | Keyword/Type      |
| ------------ | ------------------------------------ | ----------------- |
| `async`      | Declares a suspending function       | Function modifier |
| `await`      | Waits for async function to complete | Keyword           |
| `actor`      | Thread-safe state container          | Type              |
| `@MainActor` | Forces execution on main thread      | Attribute         |

---

If you want:

* A visual lifecycle diagram
* Integration with SwiftUI or UIKit
* MVVM + concurrency structure

