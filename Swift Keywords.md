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


