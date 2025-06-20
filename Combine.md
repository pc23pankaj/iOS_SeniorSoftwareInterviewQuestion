Sure! Here's a list of frequently asked **Combine framework interview questions** in Swift, ranging from beginner to advanced, including **bonus code-based scenarios**.

---

### ✅ **Basic-Level Questions**

1. **What is Combine in Swift?**

   > Explain it's a framework for handling asynchronous events using functional reactive programming.

2. **What is a `Publisher` and a `Subscriber` in Combine?**

   > Publisher emits values over time, and Subscriber receives them.

3. **What is `AnyPublisher`? Why and when do you use it?**

4. **What is a `Cancellable`? How does it work in Combine?**

5. **What are the most commonly used operators in Combine?**

   > Example: `map`, `filter`, `merge`, `flatMap`, `debounce`, `combineLatest`, etc.

6. **How is Combine different from GCD and async/await?**

---

### ✅ **Intermediate Questions**

7. **What is the difference between `@Published` and `CurrentValueSubject`?**

   > When would you use one over the other?

8. **What is `PassthroughSubject` vs `CurrentValueSubject`?**

9. **How do you handle errors in Combine?**

   * What is the `.catch` operator?
   * How does `.tryMap` differ from `.map`?

10. **What is `assign(to:on:)` vs `sink(receiveValue:)`?**

11. **What are `Schedulers` in Combine?**

* When would you use `.receive(on:)` vs `.subscribe(on:)`?

12. **Can Combine work with UIKit or SwiftUI? How?**

* Example: bind Combine publisher to a `UILabel` or `@StateObject`.

---

### ✅ **Advanced Questions**

13. **What is backpressure and demand management in Combine?**

14. **Explain memory management in Combine. How do you avoid retain cycles?**

15. **Difference between `flatMap` and `switchToLatest` in Combine?**

16. **How does Combine handle threading under the hood?**

17. **What is a `Subject` in Combine and what role does it play between Publisher and Subscriber?**

18. **How would you cancel a Combine pipeline?**

---

### 💻 Coding-Based Interview Questions

**1. Transform and filter a list of numbers using Combine:**

```swift
[1, 2, 3, 4, 5].publisher
    .filter { $0 % 2 == 0 }
    .map { $0 * 10 }
    .sink { print($0) }
```

➡️ What will this output? Why?

---

**2. Bind a `@Published` property to UI update using Combine:**

```swift
class ViewModel: ObservableObject {
    @Published var name: String = ""
}

let vm = ViewModel()
vm.$name
  .sink { print("Name changed to: \($0)") }
```

➡️ What will be printed when you change `vm.name = "Alex"`?

---

**3. FlatMap chaining with network simulation:**

```swift
func fetchUser(id: Int) -> AnyPublisher<User, Error>
func fetchPosts(user: User) -> AnyPublisher<[Post], Error>
```

➡️ How to chain these two API calls using Combine?

---

### ✨ Bonus Conceptual Questions

* How would you debounce user input in a search bar?
* What is Combine’s role in MVVM architecture?
* Can you create a custom publisher?

---

Let me know if you'd like **hands-on Combine code examples**, real use cases, or a take-home assignment-style question.
