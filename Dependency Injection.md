### What is dependency Injection in swift and how we can achieve this in simple steps?

- Dependency Injection (DI) is a design pattern used to provide objects (dependencies) that a class needs, rather than creating them inside the class itself.

> Or you can also say:

- Dependency Injection is a design pattern achieved by designing your code in a way that your objects or functions receive the objects they depend on, instead of creating their own.


**🚀 Why Use Dependency Injection?**
- ✅ Improves testability (e.g., mock dependencies in unit tests)
- ✅ Promotes loose coupling between components
- ✅ Increases flexibility and maintainability

**What is Dependency?**
- A dependency is any object a class relies on to function.

Example:

```swift
class Engine {
    func start() {
        print("Engine started")
    }
}

class Car {
    let engine = Engine() // tightly coupled
}
```
Here, Car creates its own dependency — not ideal.

**What is Dependency Injection?**
- Instead of creating the dependency, we inject it:
```swift
  class Car {
    let engine: Engine

    init(engine: Engine) { // Dependency Injection
        self.engine = engine
    }
}
```

Now Car does not create the engine; it just uses one that is passed to it.

**Types of Dependency Injection in Swift**

| Type                         | How It Works                   | Example Use |
| ---------------------------- | ------------------------------ | ----------- |
| 1. **Initializer Injection** | Passed in constructor (`init`) | ✅ Preferred |
| 2. **Property Injection**    | Assigned after initialization  | Optional    |
| 3. **Method Injection**      | Passed as method parameters    | Limited use |



**🔹 1. Initializer Injection (Recommended)**
```swift
class Logger {
    func log(_ message: String) {
        print("LOG:", message)
    }
}

class NetworkManager {
    let logger: Logger

    init(logger: Logger) {
        self.logger = logger
    }

    func fetchData() {
        logger.log("Fetching data...")
    }
}

// Inject the dependency
let logger = Logger()
let networkManager = NetworkManager(logger: logger)
networkManager.fetchData()
```

**🔹 2. Property Injection**
```swift
class Service {
    func run() { print("Service running") }
}

class Controller {
    var service: Service? // Inject after init
}

let controller = Controller()
controller.service = Service()
controller.service?.run()
```

**🔹 3. Method Injection**
```swift
class Analytics {
    func track(event: String) {
        print("Tracked:", event)
    }
}

func performLogin(analytics: Analytics) {
    // Injected only for this method
    analytics.track(event: "UserLoggedIn")
}
```


### 🔄 Bonus: Using Protocols for Better Testability

```swift
protocol EngineProtocol {
    func start()
}

class Engine: EngineProtocol {
    func start() { print("Real Engine started") }
}

class MockEngine: EngineProtocol {
    func start() { print("Mock Engine started (test)") }
}

class Car {
    let engine: EngineProtocol

    init(engine: EngineProtocol) {
        self.engine = engine
    }
}
```
Now you can inject MockEngine() for unit tests.

### ✅ Summary

| Benefit            | How DI Helps              |
| ------------------ | ------------------------- |
| Testability        | Inject mocks/fakes        |
| Decoupling         | No hardcoded dependencies |
| Flexibility        | Easy to swap components   |
| Clean Architecture | Supports SOLID principles |


