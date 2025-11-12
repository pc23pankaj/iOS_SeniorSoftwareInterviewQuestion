## 🧩 **First Round Interview Questions & Answers**

---

### **Q1. Show how to implement two buttons and one label in SwiftUI to increment and decrement a value, and update it dynamically.**

**Answer:**

```swift
import SwiftUI

struct CounterView: View {
    @State private var count = 0

    var body: some View {
        VStack(spacing: 20) {
            Text("Count: \(count)")
                .font(.largeTitle)
                .padding()

            HStack(spacing: 20) {
                Button("Decrement") {
                    count -= 1
                }
                .buttonStyle(.bordered)

                Button("Increment") {
                    count += 1
                }
                .buttonStyle(.borderedProminent)
            }
        }
        .padding()
    }
}
```

🧠 **Explanation:**

* `@State` creates a mutable source of truth for the view.
* The UI updates automatically when the `count` value changes.

---

### **Q2. How to pass data in SwiftUI?**

**Answer:**
There are several ways to pass data between views in SwiftUI:

| Method               | Usage                                      | Example                                  |
| -------------------- | ------------------------------------------ | ---------------------------------------- |
| `@State`             | For local view data                        | `@State var name = "Pankaj"`             |
| `@Binding`           | Pass data two-way between parent and child | `@Binding var name: String`              |
| `@ObservedObject`    | For passing observable class objects       | `@ObservedObject var vm = ViewModel()`   |
| `@StateObject`       | For owning the source of truth in one view | `@StateObject var vm = ViewModel()`      |
| `@EnvironmentObject` | For global shared data                     | `@EnvironmentObject var user: UserModel` |
| Parameters           | Simple one-way data passing                | `ChildView(value: someValue)`            |

---

### **Q3. What are the basics of Swift and protocols?**

**Answer:**

* **Swift Basics:**

  * Strongly typed, protocol-oriented, and safe language.
  * Supports structs, classes, enums, and generics.
  * Optionals prevent null pointer crashes.

* **Protocol:**

  * Defines a blueprint of methods or properties.
  * Similar to interfaces in other languages.

**Example:**

```swift
protocol Vehicle {
    func startEngine()
}

struct Car: Vehicle {
    func startEngine() {
        print("Engine started")
    }
}
```

---

### **Q4. Difference between UIKit and SwiftUI**

| Feature        | UIKit              | SwiftUI                               |
| -------------- | ------------------ | ------------------------------------- |
| Framework Type | Imperative         | Declarative                           |
| UI Building    | Storyboards / Code | Code only                             |
| Data Binding   | Manual             | Reactive with `@State`, `@Binding`    |
| Compatibility  | iOS 2+             | iOS 13+                               |
| Preview        | No live preview    | Live Preview in Xcode                 |
| Performance    | Mature, stable     | Lightweight, optimized for modern iOS |

---

## 🚀 **Second Round Interview Questions & Answers**

---

### **Q1. What are Closures in Swift?**

**Answer:**
Closures are self-contained blocks of functionality that can be passed around and used in code (similar to lambdas).

**Example:**

```swift
let add = { (a: Int, b: Int) -> Int in
    return a + b
}
print(add(2, 3)) // 5
```

Closures **capture** variables from their surrounding context and are commonly used in callbacks, animations, and asynchronous tasks.

---

### **Q2. What is Dependency Injection?**

**Answer:**
Dependency Injection (DI) is a design pattern where dependencies are **provided** to a class instead of being created inside it.
This improves **testability, modularity, and flexibility**.

**Example:**

```swift
protocol NetworkService {
    func fetchData()
}

class APIService: NetworkService {
    func fetchData() { print("Fetching Data...") }
}

class ViewModel {
    let service: NetworkService
    init(service: NetworkService) {
        self.service = service
    }
}
```

---

### **Q3. Explain SOLID principles**

**Answer:**

| Principle                     | Description                                             |
| ----------------------------- | ------------------------------------------------------- |
| **S** – Single Responsibility | A class should do one thing only.                       |
| **O** – Open/Closed           | Open for extension, closed for modification.            |
| **L** – Liskov Substitution   | Subclasses should replace base classes without issues.  |
| **I** – Interface Segregation | Use specific, small protocols instead of one large one. |
| **D** – Dependency Inversion  | Depend on abstractions, not concretions.                |

---

### **Q4. What do you know about MVVM Architecture?**

**Answer:**
MVVM = **Model - View - ViewModel**

* **Model:** Handles data and business logic.
* **View:** UI representation.
* **ViewModel:** Connects Model & View, provides data binding.

SwiftUI naturally supports MVVM using `@StateObject`, `@ObservedObject`, and `@Published`.

---

### **Q5. What is the View Lifecycle in SwiftUI?**

**Answer:**
SwiftUI doesn’t have a strict lifecycle like UIKit (`viewDidLoad`, etc.), but you can use:

* `onAppear()` – called when a view appears
* `onDisappear()` – called when a view disappears
* `init()` – called when the struct is created
* `task {}` – for async setup when the view loads

---

### **Q6. Explain SwiftUI briefly**

**Answer:**
SwiftUI is Apple’s declarative UI framework introduced in iOS 13 that lets developers create UI by describing **what** it should do rather than **how** it should do it.
It supports live previews, reactive updates, and cross-platform code (iOS, macOS, watchOS, tvOS).

---

### **Q7. Difference between `@State` and `@StateObject`**

| Feature   | `@State`                        | `@StateObject`                                          |
| --------- | ------------------------------- | ------------------------------------------------------- |
| Type      | Value type (struct, basic data) | Reference type (class conforming to `ObservableObject`) |
| Ownership | Owned by the view               | View owns the object                                    |
| Usage     | For simple view-local state     | For observable data model across views                  |

---

### **Q8. How to pass data from one view to another in SwiftUI?**

**Answer:**

* **Using initializer parameters**

  ```swift
  NavigationLink(destination: DetailView(value: count)) { ... }
  ```
* **Using `@Binding`**

  ```swift
  @Binding var count: Int
  ```
* **Using `@EnvironmentObject`** for global shared data.
* **Using ObservableObject + @StateObject / @ObservedObject**.

---

### **Q9. Explain the `opaque` keyword in Swift**

**Answer:**
`opaque` types hide the exact return type using `some`, ensuring **type safety** while hiding implementation details.

**Example:**

```swift
func makeView() -> some View {
    Text("Hello")
}
```

Here, `some View` means it **returns a View**, but you don’t expose whether it’s a `Text`, `VStack`, etc. This helps keep APIs clean and flexible.

---

Would you like me to format this into a **PDF / printable interview notes sheet** with clean headings and syntax highlighting (for easy revision)?
