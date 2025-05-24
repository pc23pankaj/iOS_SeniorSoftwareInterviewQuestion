# OOPS

Object-Oriented Programming (OOP or OOPS) in Swift follows the same fundamental principles as other OOP languages but with Swift's modern syntax and features.

### 🧱 4 Pillars of OOPS in Swift

| **Concept**       | **Description**                                                   | **Swift Implementation**                    |
| ----------------- | ----------------------------------------------------------------- | ------------------------------------------- |
| **Encapsulation** | Hides internal details and exposes only what's necessary.         | Use `private`, `internal`, `public`, `open` |
| **Abstraction**   | Focuses on essential features, hiding complex logic.              | Use `protocol`, `class`, `extension`        |
| **Inheritance**   | Enables one class to inherit properties and methods from another. | Use `class` and `:` syntax                  |
| **Polymorphism**  | Allows objects to be treated as instances of their parent type.   | Method overriding, protocols, typecasting   |


### ✅ Example Demonstration
```swift
// Abstraction & Protocol
protocol Vehicle {
    func startEngine()
}

// Encapsulation & Class
class Car: Vehicle {
    private var engineStarted = false   // encapsulation
    
    func startEngine() {
        engineStarted = true
        print("Engine started")
    }
    
    func isRunning() -> Bool {
        return engineStarted
    }
}

// Inheritance
class ElectricCar: Car {
    override func startEngine() {
        print("Electric engine started silently")
    }
}

// Polymorphism
let vehicles: [Vehicle] = [Car(), ElectricCar()]
for v in vehicles {
    v.startEngine()  // Dynamic method dispatch (polymorphism)
}
```
**📌 Additional Swift Features Supporting OOP**
- final keyword (prevents inheritance)
- super keyword (calls superclass methods)
- required, convenience, override initializers
- deinit for cleanup

### Explaing Polymorphism in swift and its type in swift ?
In Swift, Polymorphism allows the same method or property to behave differently based on the object’s actual type.
- There are two types of polymorphism:
  🔹 1. Compile-time Polymorphism (Static Binding / Method Overloading)

  Swift does not support method overloading by only changing return type like some other languages, but it does support overloading by different parameter types or counts.
  ✅ Example: Method Overloading (Compile-time Polymorphism)

  ```swift
  class Calculator {
    func add(a: Int, b: Int) -> Int {
        return a + b
    }

    func add(a: Double, b: Double) -> Double {
        return a + b
    }

    func add(a: Int, b: Int, c: Int) -> Int {
        return a + b + c
    }
  }
  let calc = Calculator()
  print(calc.add(a: 2, b: 3))         // 5
  print(calc.add(a: 2.5, b: 3.1))     // 5.6
  print(calc.add(a: 1, b: 2, c: 3))   // 6
  ```

###🔹 2. Runtime Polymorphism (Dynamic Binding / Method Overriding)

Achieved using inheritance and method overriding or protocol-based polymorphism.
✅ Example: Method Overriding (Runtime Polymorphism)
  ```
  class Animal {
    func speak() {
        print("Animal speaks")
    }
}

class Dog: Animal {
    override func speak() {
        print("Dog barks")
    }
}

class Cat: Animal {
    override func speak() {
        print("Cat meows")
    }
}

let animals: [Animal] = [Dog(), Cat()]

for animal in animals {
    animal.speak()  // Output depends on actual object at runtime
}

  ```
```
Output:
Dog barks
Cat meows
```
  Even though the array is of type [Animal], the actual method called depends on the runtime type (Dog or Cat), demonstrating runtime polymorphism.

** 🔁 Summary Table**
| **Polymorphism Type** | **When Resolved** | **How in Swift**                         | **Example**                               |
| --------------------- | ----------------- | ---------------------------------------- | ----------------------------------------- |
| Compile-time          | At compile time   | Method overloading (by parameter types)  | `add(a: Int, b: Int)` vs `add(a: Double)` |
| Runtime               | At runtime        | Method overriding / Protocol conformance | `animal.speak()` calls overridden method  |

