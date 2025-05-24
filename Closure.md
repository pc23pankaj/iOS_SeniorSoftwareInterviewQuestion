### What is a Closure in Swift?
- A closure is a self-contained block of functionality that can be passed around and used in your code. Closures can capture and store references to variables and constants from the context in which they’re defined.

**✅ Common Interview Questions on Closures**
| Question                                       | Description                                                                                                      |
| ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **What is a closure in Swift?**                | Explain what a closure is and how it's like a function.                                                          |
| **Difference between function and closure?**   | Closures are unnamed and can capture values; functions have names.                                               |
| **What is trailing closure syntax?**           | Used to improve readability when the last parameter is a closure.                                                |
| **Can closures capture values?**               | Yes, closures capture and store references to variables/constants from the surrounding context.                  |
| **What is a capture list in closures?**        | Used to define how values are captured (strong, weak, unowned).                                                  |
| **What is escaping vs non-escaping closure?**  | Escaping closures are stored and called later; non-escaping are called within the function body.                 |
| **What is autoclosure?**                       | Automatically creates a closure from an expression. Useful for delaying execution.                               |
| **How does retain cycle occur with closures?** | Closures capture self strongly, which may cause memory leaks. Use `[weak self]` or `[unowned self]` to avoid it. |
| **What are closure types?**                    | Global, nested, and capturing closures.                                                                          |
| **How to pass closure as parameter?**          | Like `(Int, Int) -> Bool` — a function type as a parameter.                                                      |
| **What is shorthand argument syntax?**         | Use `$0`, `$1` for quick inline closures without naming parameters.                                              |




**📌 How Closures Are Used in Swift**
| Use Case                   | Example                                                                      |
| -------------------------- | ---------------------------------------------------------------------------- |
| **As callback handlers**   | For async operations like network calls, animations, etc.                    |
| **Sorting/filtering**      | `sorted(by:)`, `filter`, `map`, `reduce` all use closures.                   |
| **Event handling**         | In SwiftUI or UIKit, closures are used to handle button taps, gestures, etc. |
| **Custom logic**           | Pass custom logic to a function for flexible behavior.                       |
| **Functional programming** | Supports functional paradigms by treating functions as first-class citizens. |


**🧪 Code Example: Basic Closure**
```
let greet = { (name: String) in
    print("Hello, \(name)")
}
greet("Alice")

```
**🧪 Example: Closure as Callback**
```
func downloadData(completion: @escaping (String) -> Void) {
    // Simulate async work
    DispatchQueue.global().async {
        let result = "Data downloaded"
        completion(result)
    }
}

downloadData { result in
    print(result)
}
```

**Why do we use [weak self] in a closure?**
- When you capture self strongly inside a closure, the closure holds a strong reference to self, and if self also holds a strong reference to the closure (like in many async tasks, timers, or delegate patterns), it creates a retain cycle (strong reference cycle). This means neither self nor the closure can be deallocated, causing a memory leak. By using [weak self], you tell the closure to capture self weakly, breaking the strong reference cycle. This means:
self inside the closure becomes an optional (self?). If self is deallocated before the closure runs, the closure won’t crash but will see self as nil. Prevents memory leaks and allows self to be released properly.

Example with [weak self] (breaks retain cycle)
```
class MyViewController {
    func fetchData() {
        networkCall { [weak self] in
            guard let self = self else { return }
            self.updateUI()
        }
    }
    func updateUI() {
        print("UI updated")
    }
}

```
**Summary:**
- Use [weak self] in closures to avoid retain cycles and memory leaks when the closure captures self and self also holds the closure.


