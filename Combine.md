Absolutely! Here's a **precise answer** to each of the Combine interview questions I listed above:

---

### ✅ **Basic-Level Questions & Answers**

1. **What is Combine in Swift?**
   ➤ A reactive framework from Apple used for handling asynchronous events via **Publishers** and **Subscribers** using declarative code.

2. **What is a Publisher and a Subscriber?**
   ➤ A **Publisher** emits values over time; a **Subscriber** receives and reacts to those values.

3. **What is `AnyPublisher`?**
   ➤ A type-erased publisher—used to hide the concrete publisher type when returning from functions.

4. **What is a `Cancellable`?**
   ➤ A token representing an active subscription. Call `.cancel()` to stop receiving values.

5. **Common Operators in Combine:**
   ➤ `map`, `filter`, `flatMap`, `combineLatest`, `merge`, `debounce`, `removeDuplicates`, `sink`.

6. **How is Combine different from GCD/async-await?**
   ➤ Combine offers **stream-based** event processing.
   ➤ GCD handles threading; **async/await** handles **one-shot** asynchronous tasks.

---

### ✅ **Intermediate-Level Questions & Answers**

7. **`@Published` vs `CurrentValueSubject`**
   ➤ `@Published` is property wrapper for `ObservableObject` (SwiftUI-friendly).
   ➤ `CurrentValueSubject` stores and emits current/latest value manually.

8. **`PassthroughSubject` vs `CurrentValueSubject`**
   ➤ `PassthroughSubject`: emits new values only (no initial value).
   ➤ `CurrentValueSubject`: always holds and emits latest value.

9. **Handling errors in Combine**
   ➤ Use `.catch` or `.tryMap`.
   ➤ `map` can't throw; `tryMap` allows throwing transformations.

10. **`assign(to:on:)` vs `sink(receiveValue:)`**
    ➤ `assign`: automatically assigns published value to a property.
    ➤ `sink`: allows custom action when value is received.

11. **Schedulers: `receive(on:)` vs `subscribe(on:)`**
    ➤ `subscribe(on:)`: affects the **upstream** (subscription logic).
    ➤ `receive(on:)`: affects the **downstream** (UI updates).

12. **Can Combine work with UIKit/SwiftUI?**
    ➤ Yes. SwiftUI automatically integrates with `@Published` and Combine.
    ➤ UIKit requires manual binding via `sink`.

---

### ✅ **Advanced-Level Questions & Answers**

13. **Backpressure & demand**
    ➤ Mechanism where a subscriber can request a specific number of items. Combine manages it behind the scenes.

14. **Memory management in Combine**
    ➤ Avoid retain cycles using `[weak self]` in `sink` or `assign`. Cancel subscriptions with `Cancellable`.

15. **`flatMap` vs `switchToLatest`**
    ➤ `flatMap`: runs all inner publishers concurrently.
    ➤ `switchToLatest`: only keeps the latest inner publisher active.

16. **Combine and threading**
    ➤ Combine is **not thread-safe by default**. You must manage execution via `subscribe(on:)` and `receive(on:)`.

17. **What is a `Subject`?**
    ➤ A bridge that acts as both **Publisher and Subscriber**. Useful for sending values manually.

18. **How to cancel a pipeline?**
    ➤ Store the `Cancellable` returned by `sink` or `assign`, then call `.cancel()` when needed.

---

### 💻 **Code-Based Questions & Answers**

**1. Filter & Transform using Combine:**

```swift
[1, 2, 3, 4, 5].publisher
    .filter { $0 % 2 == 0 }
    .map { $0 * 10 }
    .sink { print($0) }
```

🟢 **Output**:

```
20  
40
```

---

**2. `@Published` usage:**

```swift
class ViewModel: ObservableObject {
    @Published var name: String = ""
}

let vm = ViewModel()
vm.$name
  .sink { print("Name changed to: \($0)") }

vm.name = "Alex"
```

🟢 **Output**:

```
Name changed to:  
Name changed to: Alex
```

---

**3. Chaining API calls:**

```swift
fetchUser(id: 1)
    .flatMap { user in
        fetchPosts(user: user)
    }
    .sink(receiveCompletion: { _ in }, receiveValue: { posts in
        print(posts)
    })
```

🟢 `flatMap` is used to chain publishers.

---

### ✨ **Bonus Conceptual Q\&A**

**Debounce user input?**

```swift
textPublisher
    .debounce(for: .milliseconds(300), scheduler: RunLoop.main)
    .sink { text in search(text) }
```

**Role of Combine in MVVM?**
➤ Combine binds `@Published` data from ViewModel to SwiftUI View (`ObservableObject`), enabling reactivity.

**Can you create a custom publisher?**
➤ Yes. Use `Publisher` protocol or `AnyPublisher` for custom logic. Also possible using `Deferred` or `Future`.

---

Would you like me to generate a sample **Combine-based take-home assignment** or **mock interview scenario** next?
