The **SOLID principles** are five design principles that help make software more understandable, flexible, and maintainable. These principles are widely used in **object-oriented programming**, including **Swift**.

### 🔤 SOLID stands for:

| Letter | Principle                             | Meaning                                                                      |
| ------ | ------------------------------------- | ---------------------------------------------------------------------------- |
| S      | Single Responsibility Principle (SRP) | One class should have one reason to change.                                  |
| O      | Open/Closed Principle (OCP)           | Software entities should be open for extension, but closed for modification. |
| L      | Liskov Substitution Principle (LSP)   | Subtypes must be substitutable for their base types.                         |
| I      | Interface Segregation Principle (ISP) | Prefer many specific interfaces over a single general-purpose one.           |
| D      | Dependency Inversion Principle (DIP)  | Depend on abstractions, not on concrete implementations.                     |

---

## ✅ 1. **S** – Single Responsibility Principle

**Definition:** A class should have **only one reason to change**.
**Means:** Each class should do **only one thing**.

### 🧑‍💻 Example:

```swift
// ❌ Bad: One class does two things – manage user data and save to file
class UserManager {
    func createUser(name: String) {
        // logic to create user
    }
    
    func saveToFile(user: String) {
        // logic to save user to file
    }
}

// ✅ Good: Separate responsibilities
class UserCreator {
    func createUser(name: String) {
        // logic to create user
    }
}

class UserSaver {
    func saveToFile(user: String) {
        // logic to save user to file
    }
}
```

---

## ✅ 2. **O** – Open/Closed Principle

**Definition:** Classes should be **open for extension** but **closed for modification**.

### 🧑‍💻 Example:

```swift
// ❌ Bad: Modify existing code to add new discount logic
class Discount {
    func calculate(price: Double, type: String) -> Double {
        if type == "Student" {
            return price * 0.9
        } else if type == "Senior" {
            return price * 0.8
        } else {
            return price
        }
    }
}

// ✅ Good: Extend using protocol
protocol DiscountStrategy {
    func apply(to price: Double) -> Double
}

class StudentDiscount: DiscountStrategy {
    func apply(to price: Double) -> Double { price * 0.9 }
}

class SeniorDiscount: DiscountStrategy {
    func apply(to price: Double) -> Double { price * 0.8 }
}

class NoDiscount: DiscountStrategy {
    func apply(to price: Double) -> Double { price }
}

class Checkout {
    func finalPrice(price: Double, discount: DiscountStrategy) -> Double {
        discount.apply(to: price)
    }
}
```

---

## ✅ 3. **L** – Liskov Substitution Principle

**Definition:** Subtypes must be substitutable for their base types without altering the correctness of the program.

### 🧑‍💻 Example:

```swift
class Bird {
    func fly() {
        print("Flying")
    }
}

// ❌ Bad: Ostrich can't fly, violates substitution
class Ostrich: Bird {
    override func fly() {
        fatalError("Ostrich can't fly!")
    }
}

// ✅ Good: Restructure using protocol
protocol Bird {
    func layEgg()
}

protocol Flyable {
    func fly()
}

class Sparrow: Bird, Flyable {
    func layEgg() {}
    func fly() { print("Flying") }
}

class Ostrich: Bird {
    func layEgg() {}
}
```

---

## ✅ 4. **I** – Interface Segregation Principle

**Definition:** A client should not be forced to depend on interfaces it doesn't use.

### 🧑‍💻 Example:

```swift
// ❌ Bad: A printer that forces all classes to implement all methods
protocol Machine {
    func printDoc()
    func scanDoc()
    func faxDoc()
}

// ❌ Not all machines can fax or scan
class OldPrinter: Machine {
    func printDoc() { print("Print") }
    func scanDoc() { /* Not supported */ }
    func faxDoc() { /* Not supported */ }
}

// ✅ Good: Split into multiple interfaces
protocol Printer {
    func printDoc()
}

protocol Scanner {
    func scanDoc()
}

class SimplePrinter: Printer {
    func printDoc() { print("Printing...") }
}

class MultiFunctionPrinter: Printer, Scanner {
    func printDoc() { print("Print") }
    func scanDoc() { print("Scan") }
}
```

---

## ✅ 5. **D** – Dependency Inversion Principle

**Definition:** High-level modules should not depend on low-level modules. Both should depend on abstractions.

### 🧑‍💻 Example:

```swift
// ❌ Bad: High-level class depends on concrete class
class FileLogger {
    func log(message: String) {
        print("Log: \(message)")
    }
}

class App {
    let logger = FileLogger()
    
    func run() {
        logger.log(message: "App started")
    }
}

// ✅ Good: Use abstraction (protocol)
protocol Logger {
    func log(message: String)
}

class ConsoleLogger: Logger {
    func log(message: String) {
        print("Console: \(message)")
    }
}

class FileLogger: Logger {
    func log(message: String) {
        print("File: \(message)")
    }
}

class App {
    let logger: Logger
    
    init(logger: Logger) {
        self.logger = logger
    }
    
    func run() {
        logger.log(message: "App started")
    }
}
```

---

## ✅ Summary Table

| Principle                     | Meaning                          | Focus            |
| ----------------------------- | -------------------------------- | ---------------- |
| **S** - Single Responsibility | One reason to change             | Cohesion         |
| **O** - Open/Closed           | Extend without modifying         | Extensibility    |
| **L** - Liskov Substitution   | Replace parent with child safely | Substitutability |
| **I** - Interface Segregation | Specific interfaces preferred    | Decoupling       |
| **D** - Dependency Inversion  | Depend on abstractions           | Flexibility      |

