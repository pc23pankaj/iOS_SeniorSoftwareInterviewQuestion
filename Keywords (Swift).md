## Final 
In Swift, the `**final**` keyword is used to **prevent inheritance or overriding**.

---

## ✅ `final` in Swift — What It Means:

| Usage               | Prevents                              |
| ------------------- | ------------------------------------- |
| `final class`       | Prevents subclassing (no inheritance) |
| `final func`        | Prevents overriding in subclasses     |
| `final var` / `let` | Prevents overriding computed property |

---

## 🔒 1. **Final Class**

Prevents any other class from inheriting from it.

```swift
final class Animal {
    func speak() {
        print("Some sound")
    }
}

// ❌ Error: Cannot inherit from final class
// class Dog: Animal {} 
```

---

## 🔒 2. **Final Method or Property**

Prevents the method/property from being overridden in a subclass.

```swift
class Vehicle {
    final func start() {
        print("Starting engine")
    }
}

// ❌ Error: Cannot override 'start' because it's final
class Car: Vehicle {
    // override func start() { ... } 
}
```

---

## 🧠 Why Use `final`?

* ✅ **Performance**: Compiler can optimize better because it knows the method/class won't change.
* ✅ **Safety**: Prevents unintended behavior from subclassing or overriding.

---

## 📌 Summary:

| `final` Used On | Prevents                   |
| --------------- | -------------------------- |
| `class`         | Subclassing                |
| `func`          | Overriding                 |
| `var`/`let`     | Overriding computed values |

Let me know if you want an example comparing `final` vs `override`!



## Why Use inout?
- By default, Swift passes arguments by value (a copy), so changes inside a function don’t affect the original. inout allows you to modify the passed variable directly.
```
✅ Basic Example:
func addFive(to number: inout Int) {
    number += 5
}

var myNumber = 10
addFive(to: &myNumber)
print(myNumber) // Output: 15
```
**🔹 Notes:**
The parameter is marked inout in the function definition
When calling the function, use & before the variable

Absolutely! Here’s a **handy list of common Swift keywords** and their **meanings**, especially useful for interviews or brushing up on the basics:

---

## ✅ **Common Swift Keywords and Their Meaning**

| **Keyword**                                                                 | **Meaning / Use**                                                            |
| --------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `var`                                                                       | Declares a **mutable** variable (can be changed)                             |
| `let`                                                                       | Declares a **constant** (cannot be changed once set)                         |
| `func`                                                                      | Declares a **function**                                                      |
| `class`                                                                     | Defines a **reference type** object                                          |
| `struct`                                                                    | Defines a **value type** object                                              |
| `enum`                                                                      | Defines an **enumeration** (a list of related values)                        |
| `protocol`                                                                  | Defines a **blueprint** of methods or properties for conformance             |
| `extension`                                                                 | Adds new functionality to existing types                                     |
| `init`                                                                      | **Initializer/constructor** for setting up an instance                       |
| `deinit`                                                                    | **Deinitializer** for cleanup before an object is deallocated                |
| `self`                                                                      | Refers to the **current instance** of the type                               |
| `super`                                                                     | Refers to the **superclass** of the current class                            |
| `guard`                                                                     | Used for **early exit** if a condition is not met                            |
| `if`, `else`                                                                | Conditional branching                                                        |
| `switch`                                                                    | Used for multiple condition handling                                         |
| `for-in`                                                                    | Looping over collections or ranges                                           |
| `while`, `repeat`                                                           | Looping with conditions                                                      |
| `break`                                                                     | Exits a loop or switch                                                       |
| `continue`                                                                  | Skips to the next loop iteration                                             |
| `return`                                                                    | Returns a value from a function                                              |
| `throw`, `try`, `catch`                                                     | Used for **error handling**                                                  |
| `do`                                                                        | Used with `try` for error-handling blocks                                    |
| `as`, `is`                                                                  | **Type casting** and type checking                                           |
| `inout`                                                                     | Passes a variable **by reference**, allowing it to be modified in a function |
| `final`                                                                     | Prevents further subclassing or overriding                                   |
| `lazy`                                                                      | Delays the initialization of a property until it's first used                |
| `static`                                                                    | Declares a type-level property or method (shared by all instances)           |
| `mutating`                                                                  | Allows a `struct` or `enum` method to **modify `self`**                      |
| `defer`                                                                     | Postpones code to run **just before scope exits**                            |
| `weak`, `unowned`                                                           | Reference qualifiers to avoid retain cycles in ARC                           |
| `@State`, `@Binding`, `@Published`, `@ObservedObject`, `@EnvironmentObject` | SwiftUI & Combine property wrappers for data-driven UI                       |
| `await`, `async`                                                            | Used for **concurrent/asynchronous** code execution (Swift Concurrency)      |

---

| **Term** | **Meaning**                                                                                | **Used Where?**                             | **Example**                  |
| -------- | ------------------------------------------------------------------------------------------ | ------------------------------------------- | ---------------------------- |
| `self`   | Refers to the **current instance** of a type (object, struct, etc.)                        | Inside instance methods, initializers       | `self.name = name`           |
| `Self`   | Refers to the **type itself** (class/struct/enum) — like a placeholder for the actual type | In protocols, return types, static contexts | `static func make() -> Self` |


| **Operator** | **Meaning** | **Applies To**                                                   | **Checks**                                                 |
| ------------ | ----------- | ---------------------------------------------------------------- | ---------------------------------------------------------- |
| `==`         | Equality    | All `Equatable` types (structs, enums, classes with conformance) | **Value equality**                                         |
| `===`        | Identity    | **Only classes**                                                 | If **two references** point to the **exact same instance** |

| **Protocol** | **Definition**                                                    | **Purpose**                                                   | **Synthesized Automatically?**            | **Usage Example**                                   |
| ------------ | ----------------------------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------- | --------------------------------------------------- |
| `Equatable`  | Allows comparing two values using `==`                            | Check if two instances are equal                              | ✅ (for structs with Equatable properties) | `a == b`                                            |
| `Hashable`   | Allows a type to be stored in a `Set` or used as a dictionary key | Generate a unique hash value                                  | ✅ (for structs with Hashable properties)  | `Set`, `Dictionary` keys                            |
| `Codable`    | Combines `Encodable` and `Decodable`                              | Convert between Swift types and external formats (e.g., JSON) | ✅ (if all properties conform)             | `JSONDecoder().decode()` / `JSONEncoder().encode()` |
| `Decodable`  | Parses external formats (like JSON) into Swift types              | Deserialize from JSON → Swift                                 | ✅                                         | `JSONDecoder().decode()`                            |
| `Encodable`  | Converts Swift types to external formats (like JSON)              | Serialize Swift → JSON                                        | ✅                                         | `JSONEncoder().encode()`                            |

