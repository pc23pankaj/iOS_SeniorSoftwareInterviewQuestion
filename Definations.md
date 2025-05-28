# ✅ Swift Core Concepts & Memory Management

---

## 🔁 Generic
**Generic** allows you to write flexible, reusable functions and types that work with any data type.

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temp = a
    a = b
    b = temp
}
```

## 🧺 Tuple

A **Tuple** is a group of multiple values combined into a single compound value. Useful for returning multiple values from a function.

```
let person = (name: "Alice", age: 30)
print(person.name) // Alice

```

## 📦 Enum

**Enum** defines a common type for a group of related values and enables you to work with those values in a type-safe way.
```
enum Result {
    case success(String)
    case failure(Error)
}

```


## 🧩 Extension

**Extension** adds new functionality to an existing class, structure, enumeration, or protocol without modifying the original source code.
```
extension String {
    var isEmail: Bool { self.contains("@") }
}

```

## 🧠 Memory Management Concepts

### 🟢 Strong

Strong references keep an object alive by increasing its retain count.
```
class A {
    var b: B? // Strong by default
}
```
### 🟡 Weak

Weak references do not increase the retain count, allowing the object to be deallocated. Must be optional.

```
class A {
    weak var b: B?
}

```

### 🔴 Unowned

Unowned is like weak but non-optional. Use when the reference is expected to always have a value during its lifetime.

```
class A {
    unowned var b: B
}

```

## ⚙️ Thread Safety: Atomic vs Non-Atomic

### 🧷 Atomic

Atomic properties are thread-safe—only one thread can access them at a time. Not natively supported in Swift but can be implemented using DispatchQueue.

```
private let queue = DispatchQueue(label: "atomic.queue")
var _name: String = ""
var name: String {
    get {
        queue.sync { _name }
    }
    set {
        queue.sync { _name = newValue }
    }
}

```


### ⚡ Non-Atomic

Non-Atomic properties are not thread-safe, meaning multiple threads can read/write at the same time. Faster, but unsafe in multithreaded contexts.


### 🧮 Retain Count

Retain Count is the number of strong references to an object. When it drops to zero, the object is deallocated.

Obj-c 
```
CFGetRetainCount(object);
```
