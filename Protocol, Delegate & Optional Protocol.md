In Swift, **protocols** define a blueprint of methods or properties, and conforming types **must implement** all required parts. But sometimes, you want to make **some protocol methods optional** — that’s called an **optional protocol**.

## What is a Delegate?
A delegate is an instance (usually a view controller or manager) that conforms to a protocol and is assigned to handle events or send back data from another class.
---

## ✅ What Is an Optional Protocol?

An **optional protocol** lets conforming types choose **whether or not** to implement certain methods or properties.

---

## 🧩 But Swift Protocols Don't Support `optional` by Default — So How Can You Do It?

---

### ✅ 1. **Using `@objc` + `optional` (Objective-C Compatibility)**

This is the **only way** to use the `optional` keyword directly.

```swift
@objc protocol MyDelegate {
    @objc optional func didTapButton()
    @objc optional var title: String? { get }
}
```

#### 🔸 Requirements:

* Protocol must be marked with `@objc`
* Only works for **classes** (not structs or enums)
* Must conform to `NSObjectProtocol` or be used in Objective-C-compatible classes

#### 🔸 Example:

```swift
class ViewController: NSObject, MyDelegate {
    func didTapButton() {
        print("Button tapped")
    }
}
```

---

### ✅ 2. **Use Default Implementations (Protocol Extension)**

This is the **Swifty way** to achieve "optional-like" behavior.

```swift
protocol MyProtocol {
    func requiredMethod()
    func optionalMethod()
}

extension MyProtocol {
    func optionalMethod() {
        // Default implementation (can be empty)
    }
}
```

#### 🔸 Example:

```swift
class MyClass: MyProtocol {
    func requiredMethod() {
        print("I must implement this")
    }

    // optionalMethod() is optional due to default implementation
}
```

> ✅ Works with **structs, enums, and classes**
> ✅ **Compile-time safety** (unlike `@objc` optional which needs optional chaining)

---

### ✅ 3. **Use Closures as Optional Callbacks**

Instead of optional methods, you can use **optional closures**:

```swift
protocol Downloader {
    var onComplete: (() -> Void)? { get set }
}
```

Then:

```swift
class ImageDownloader: Downloader {
    var onComplete: (() -> Void)?

    func download() {
        // ...
        onComplete?()
    }
}
```

> ✅ Clean and **decoupled**
> ✅ Ideal for **callback/event handling**

---

## 🧠 Summary Table:

| Method                      | Works with | Optional Support | Notes                                    |
| --------------------------- | ---------- | ---------------- | ---------------------------------------- |
| `@objc` + `optional`        | Classes    | ✅ Yes            | Requires `@objc`, runtime checking       |
| Protocol Extension Defaults | All types  | ✅ Yes (default)  | Compile-time safety, Swifty              |
| Optional Closures           | All types  | ✅ Yes            | Best for events, no need for inheritance |

---

Let me know if you want real-life use cases — like making a delegate optional in a view controller!
