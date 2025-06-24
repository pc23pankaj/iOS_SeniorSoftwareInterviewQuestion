# ✅ Swift Core Concepts & Memory Management

---
## Static 
**🔍 In Detail**
- When you mark something as static, it means you access it using the type name, not an object created from the type.
- It is shared across all instances (if any exist at all).
- Commonly used for constants, counters, configuration values, or utility methods.
  
> static means the property or method is shared and does not require an instance. It’s a type-level member.

### 📌 static vs class (for reference)
**static** — works for structs, enums, and classes.
**class** — only for classes and can be overridden in subclasses:

| Keyword      | Mutable?             | Value Can Be Changed? | Thread-Safe? (By default)                        |
| ------------ | ---------------------| --------------------- | ---------------------------------------------    |
| `static let` | ❌ No   (read Only)  | ❌ No                | ✅ Yes (because it's constant)                   |
| `static var` | ✅ Yes  (read/write) | ✅ Yes               | ❌ No (needs protection in multithreaded code)   |




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
### Q. What’s retain cycle how you can avoid
**Ans.** Retain cycle is a memory management issue where objects reference each other and cannot be released. It can be avoided by using weak or unowned references.
- Retain cycle occurs when two or more objects hold strong references to each other.
- To avoid retain cycle, use weak or unowned references instead of strong references.
- Weak references do not increase the reference count of an object and automatically become nil when the object is deallocated.
- Unowned references are similar to weak references but are assumed to always have a value and do not become nil when the object is deallocated.

Obj-c 
```
CFGetRetainCount(object);
```

### Q. What is KVC and KVO? Give an example of using KVC to set a value.
- **KVC stands for Key-Value Coding.** It's a mechanism by which an object's properties can be accessed using string's at runtime rather than having to statically know the property names at development time. 
- **KVO stands for Key-Value Observing Key-value** observing is a mechanism that enables an object to be notified directly when a property of another object changes.

### Q. Lazy 
- A **lazy** stored property is a property whose initial value isn't calculated until the first time it's used. ... You must always declare a lazy property as a variable (with the var keyword), because its initial value might not be retrieved until after instance initialization completes.


### Q. typealias
-A **typealias** is a keyword used to define an alias or alternative name for an existing type.
✅ Purpose of typealias
Improves readability of complex types.
Provides abstraction or semantic meaning to a type.
Helps shorten long generic or closure types.

