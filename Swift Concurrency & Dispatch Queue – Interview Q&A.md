# 🚦 iOS Multithreading & Concurrency Guide

## ❓ Frequently Asked Questions

### 1. What is `DispatchQueue` in Swift?

`DispatchQueue` is a part of **GCD (Grand Central Dispatch)**, used to manage concurrent tasks in your app.

---

### 2. What is the difference between `main` and `global` queues?

| Queue         | Description                                                |
|---------------|------------------------------------------------------------|
| `DispatchQueue.main`  | Runs tasks on the **main thread**, used for UI updates.         |
| `DispatchQueue.global()` | Runs tasks on a **background thread**, ideal for heavy tasks. |

---

### 3. What is the difference between `async` and `sync`?

| Keyword | Behavior                                                    |
|---------|-------------------------------------------------------------|
| `async` | Executes the task **asynchronously** (non-blocking).        |
| `sync`  | Executes the task **synchronously** (blocking).             |

**Example**:
```swift
DispatchQueue.global().async {
    // Background thread
    DispatchQueue.main.async {
        // Back to main thread for UI updates
    }
}

4. What is DispatchSemaphore?
DispatchSemaphore is used for synchronization between threads, controlling access to resources.
Example:
