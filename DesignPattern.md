Design patterns in Swift (or any language) are general, reusable solutions to common problems in software design. They are not finished code but templates for how to solve a problem in various contexts. Swift, being a modern language with OOP and protocol-oriented paradigms, supports a wide variety of design patterns.

Here’s a categorized breakdown of the most commonly used **design patterns in Swift**:

---

## ✅ **1. Creational Patterns**

These deal with object creation mechanisms.

### a. **Singleton**

Ensures a class has only one instance and provides a global access point.

```swift
class NetworkManager {
    static let shared = NetworkManager()
    private init() { }
}
```

### b. **Factory Method**

Defines an interface for creating an object but lets subclasses alter the type of objects.

```swift
protocol Button {
    func render()
}

class iOSButton: Button {
    func render() { print("iOS Button") }
}

class ButtonFactory {
    static func createButton(for platform: String) -> Button {
        return platform == "iOS" ? iOSButton() : AndroidButton()
    }
}
```

### c. **Builder**

Constructs a complex object step-by-step.

```swift
struct Pizza {
    var cheese = false
    var pepperoni = false
}

class PizzaBuilder {
    private var pizza = Pizza()
    func addCheese() -> PizzaBuilder {
        pizza.cheese = true
        return self
    }
    func addPepperoni() -> PizzaBuilder {
        pizza.pepperoni = true
        return self
    }
    func build() -> Pizza {
        return pizza
    }
}
```

---

## ✅ **2. Structural Patterns**

These help ensure components are well structured and work together.

### a. **Adapter**

Allows incompatible interfaces to work together.

```swift
protocol Bird {
    func fly()
}

class Sparrow: Bird {
    func fly() { print("Flying") }
}

class ToyDuck {
    func squeak() { print("Squeak") }
}

class BirdAdapter: ToyDuck {
    private var bird: Bird
    init(bird: Bird) { self.bird = bird }
    override func squeak() {
        bird.fly() // adapting fly to squeak
    }
}
```

### b. **Decorator**

Adds behavior to objects dynamically.

```swift
protocol Coffee {
    func cost() -> Int
}

class BasicCoffee: Coffee {
    func cost() -> Int { return 5 }
}

class MilkDecorator: Coffee {
    private var base: Coffee
    init(base: Coffee) { self.base = base }
    func cost() -> Int { return base.cost() + 2 }
}
```

### c. **Facade**

Provides a simplified interface to a complex subsystem.

```swift
class Engine { func start() { print("Engine started") } }
class Lights { func on() { print("Lights on") } }

class CarFacade {
    private let engine = Engine()
    private let lights = Lights()
    func startCar() {
        lights.on()
        engine.start()
    }
}
```

---

## ✅ **3. Behavioral Patterns**

These are concerned with communication between objects.

### a. **Observer**

An object maintains a list of dependents and notifies them of changes.

```swift
protocol Observer: AnyObject {
    func update()
}

class Subject {
    private var observers = [Observer]()
    func add(observer: Observer) { observers.append(observer) }
    func notify() { observers.forEach { $0.update() } }
}
```

### b. **Strategy**

Encapsulates interchangeable behaviors and uses delegation.

```swift
protocol SortStrategy {
    func sort(_ data: [Int]) -> [Int]
}

class QuickSort: SortStrategy {
    func sort(_ data: [Int]) -> [Int] { return data.sorted() }
}

class Sorter {
    var strategy: SortStrategy
    init(strategy: SortStrategy) {
        self.strategy = strategy
    }
    func sort(data: [Int]) -> [Int] {
        return strategy.sort(data)
    }
}
```

### c. **Command**

Encapsulates a request as an object.

```swift
protocol Command {
    func execute()
}

class Light {
    func turnOn() { print("Light On") }
}

class LightOnCommand: Command {
    let light: Light
    init(light: Light) { self.light = light }
    func execute() { light.turnOn() }
}
```

---

## ✅ **4. Protocol-Oriented Patterns (Swift-specific)**

### a. **Delegation (via Protocols)**

```swift
protocol DownloadDelegate: AnyObject {
    func didFinishDownload()
}

class Downloader {
    weak var delegate: DownloadDelegate?
    func start() {
        // download complete
        delegate?.didFinishDownload()
    }
}
```

### b. **Coordinator Pattern**

Used for navigation logic in iOS apps, especially in UIKit-based projects.

---

## ✅ Summary Table

| Category     | Pattern             | Use Case Example                              |
| ------------ | ------------------- | --------------------------------------------- |
| Creational   | Singleton           | Shared services, e.g., `UserDefaults`         |
| Structural   | Adapter             | Wrapping incompatible APIs                    |
| Behavioral   | Observer            | `@Published` in `Combine`, NotificationCenter |
| Swift Native | Protocol Delegation | TableView delegate methods                    |

---

If you want real-world usage examples for iOS apps or SwiftUI architecture (like MVVM, Redux, etc.), let me know.
