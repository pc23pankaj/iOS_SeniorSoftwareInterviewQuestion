### 🚦 iOS Multithreading & Concurrency Guide


### Q 1. What is `DispatchQueue` in Swift?

`DispatchQueue` is a part of **GCD (Grand Central Dispatch)**, used to manage concurrent tasks in your app.

---


### Q 2. What is the difference between `main` and `global` queues?

| Queue         | Description                                                |
|---------------|------------------------------------------------------------|
| `DispatchQueue.main`  | Runs tasks on the **main thread**, used for UI updates.         |
| `DispatchQueue.global()` | Runs tasks on a **background thread**, ideal for heavy tasks. |

---


### Q 3. What is the difference between `async` and `sync`?

| Keyword | Behavior                                                    |
|---------|-------------------------------------------------------------|
| `async` | Executes the task **asynchronously** (non-blocking).        |
| `sync`  | Executes the task **synchronously** (blocking).             |

**Example** :
```swift 
DispatchQueue.global().async {
// Background thread
DispatchQueue.main.async {
// Back to main thread for UI updates
}
}
```


### Q 4. What is DispatchSemaphore?
DispatchSemaphore is used for synchronization between threads, controlling access to resources.

**Example** : 

```swift 
let semaphore = DispatchSemaphore(value: 1)
DispatchQueue.global().async {
    semaphore.wait()  // ↓ wait for resource
    // critical section
    semaphore.signal() // ↑ release resource
}
```


### 🔄 From Dispatch Queues to Concurrency Concepts

### Q5. What is Concurrency?**
- Concurrency is the ability to run multiple tasks at overlapping time periods, not necessarily simultaneously.



### Q6. What is Parallelism?**
- Parallelism is the true simultaneous execution of multiple tasks using multiple cores.



### Q7. What is Context Switching?**
- Context Switching is the process of switching between threads or tasks, which incurs CPU overhead.

### **Advantage over each other:**

| **Aspect**                    | **GCD Advantages over NSOperation**               | **NSOperation Advantages over GCD**                              |
| ----------------------------- | ------------------------------------------------- | ---------------------------------------------------------------- |
| **Implementation**            | Very lightweight and simple to implement          | NSOperationQueue is complex and heavier                          |
| **Control on Operation**      | Limited control (no pause, resume, cancel easily) | You can pause, cancel, and resume operations                     |
| **Dependencies**              | No built-in support for dependencies              | Supports dependencies; operations wait until dependencies finish |
| **State Monitoring**          | Cannot monitor operation state                    | Can monitor states: ready, executing, finished                   |
| **Max Concurrent Operations** | No direct max operation limit control             | Can specify max number of concurrent operations                  |




### Q 8. ⚙️ GCD vs NSOperation

| **Feature**       | GCD (Grand Central Dispatch) | NSOperation / OperationQueue                    |
| ----------------- | ---------------------------- | ----------------------------------------------- |
| Abstraction Level | Low-level, C-based API       | High-level, Objective-C / Swift API             |
| Customization     | Limited                      | Supports dependencies, priorities, cancellation |
| Reusability       | Hard to reuse blocks         | Can subclass NSOperation for reusable logic     |
| KVO Support       | ❌ No                         | ✅ Yes                                         |
| Cancellation      | ❌ No (hard to cancel blocks) | ✅ Yes                                        |





### Q 9. ✅ Advantages and 🚫 Disadvantages

| **GCD**                                         |  NSOperation                                    |
| ----------------------------------------------- | ----------------------------------------------- |
| ✅ Simple syntax                                | ✅ Supports cancellation, dependencies          |
| ✅ Lightweight                                  | ✅ Better for complex task management           |
| 🚫 No built-in cancellation                     | 🚫 More boilerplate                             |
| 🚫 Harder to manage complex dependencies        | 🚫 Slightly heavier than GCD                    |




### Q 10. (Quality of Service) QOS 

| **QoS Class**       | **Priority**     | **Typical Use Cases**                                        |
| ------------------- | ---------------- | ------------------------------------------------------------ |
| **userInteractive** | Highest priority | UI updates, animations, event handling                       |
| **userInitiated**   | High priority    | Tasks triggered by user actions needing quick results        |
| **utility**         | Low priority     | Downloads, file I/O, background computations with progress   |
| **background**      | Lowest priority  | Pre-fetching, backups, maintenance tasks that don’t block UI |


### Q 11. How GCD Schedules Tasks on the Global Queue Across Multiple CPU Cores?
- **Global Queue is Concurrent:** The global queue is a concurrent queue, meaning it can run multiple tasks at the same time.
- **System-Managed Thread Pool:** GCD maintains an internal thread pool managed by the system. It dynamically adjusts the number of threads based on system resources and workload.
- **Automatic Core Utilization:** When you dispatch tasks to the global queue, GCD schedules them across available CPU cores to maximize parallelism and performance.
- **Work Stealing and Load Balancing:** GCD uses work stealing to balance the load between threads. If one thread finishes its tasks early, it can "steal" tasks from busier threads to keep all cores busy.
- **Quality of Service (QoS) Influences Scheduling:** Tasks with higher QoS get preference on CPU time and resource allocation.
- **Context Switching Managed by System:** The OS handles context switching between threads to efficiently share CPU time when there are more tasks than available cores.


### Q12. ✅ What is DispatchWorkItem?
- **DispatchWorkItem** is a wrapper for a block of code that can be dispatched to a queue. It allows you to manage, cancel, and monitor the execution of that block more flexibly than simply using DispatchQueue.async.

## 🔧 Why Use DispatchWorkItem?
You use DispatchWorkItem when you need:
    - Cancelable tasks
    - Reusability
    - Notification when task completes
    - Barrier control in concurrent queues
    - Pre-configured blocks to be dispatched later
    
**🧠 Basic Syntax:**
```
let workItem = DispatchWorkItem {
    print("Task is running")
}

DispatchQueue.global().async(execute: workItem)
```
>**🧪 Example 1: Canceling a Task**
```
let task = DispatchWorkItem {
    for i in 0..<10 {
        if task.isCancelled { return }
        print(i)
    }
}

DispatchQueue.global().async(execute: task)

// Cancel it after 0.1s
DispatchQueue.global().asyncAfter(deadline: .now() + 0.1) {
    task.cancel()
}
```
>**🧪 Example 2: Notify When Finished**
```
let workItem = DispatchWorkItem {
    // Long running task
    sleep(2)
    print("Finished task")
}

DispatchQueue.global().async(execute: workItem)

workItem.notify(queue: .main) {
    print("Update UI now!")
}
```

>**🧪 Example 3: Delayed Dispatch**
```
let delayedItem = DispatchWorkItem {
    print("Executed after delay")
}

DispatchQueue.main.asyncAfter(deadline: .now() + 2, execute: delayedItem)
```

## 🚨 When to Use DispatchWorkItem

| Use Case                                      | Prefer `DispatchWorkItem` Over |
| --------------------------------------------- | ------------------------------ |
| You need to cancel work                       | `DispatchQueue.async {}`       |
| You want to observe completion                | Simple GCD block               |
| You want delayed dispatch with cancel support | `asyncAfter`                   |
| You want more control over execution          | Traditional GCD blocks         |


## 🔚 Summary
DispatchWorkItem gives more control than plain GCD blocks:
Cancelable
Notifiable
Reusable
Monitored
Perfect for tasks that are potentially long-running, UI-related, or need to be canceled or delayed with precision.





**Method Dispatch** is the process Swift uses to determine which specific function implementation to execute when a method is called. The two main types are **Static Dispatch** and **Dynamic Dispatch**, representing a trade-off between performance and flexibility.

-----

## **1. Static Dispatch (Direct/Compile-Time)** 🚀

Static dispatch means the exact function to be called is decided and its memory address is directly referenced at **compile time**.

  * **Resolution:** **Compile Time.** The compiler embeds the function's memory address into the compiled code.
  * **Performance:** It's the **fastest** form of dispatch because the program jumps directly to the function's memory location with **zero runtime overhead**. It also enables compiler optimizations like **inlining**.
  * **Used For:**
      * Methods on **value types** (**Structs** and **Enums**), as they do not support inheritance.
      * Methods or classes marked with the **`final`** keyword (prevents overriding).
      * Methods in **protocol extensions** that are *not* part of the protocol's required methods.

### **Example**

```swift
struct Point { // Value Type
    func getX() -> Int {
        return 10
    }
}

final class FixedEngine { // final Class
    func start() { /* ... */ } // Static dispatch
}

let p = Point()
p.getX() // Static Dispatch
```

-----

## **2. Dynamic Dispatch (Table/Run-Time)** 🔄

Dynamic dispatch means the function to be called is determined at **run time**, based on the actual type of the object, which is necessary to support polymorphism (method overriding).

  * **Resolution:** **Run Time.** The program must perform a lookup.
  * **Mechanism:** Swift primarily uses **Table Dispatch**.
      * For **Classes**, it uses a **Virtual Table (V-Table)** of function pointers.
      * For **Protocols**, it uses a **Witness Table** to map protocol requirements to the conforming type's implementation.
  * **Performance:** It is **slower** than static dispatch due to the required runtime lookup (indirection) but provides maximum **flexibility**.
  * **Used For:**
      * **Overridable methods in classes** (those not marked `final`).
      * Method calls made through a **Protocol** type (e.g., `let drawable: any Drawable = Circle()`).

### **Example (V-Table for Classes)**

```swift
class Vehicle {
    func start() {
        print("Vehicle started.")
    }
}

class Car: Vehicle {
    override func start() { // Overridden method
        print("Car engine roared!")
    }
}

let myVehicle: Vehicle = Car()
// Dynamic dispatch: The V-Table is checked at runtime to call Car's implementation.
myVehicle.start() // Output: "Car engine roared!"
```

-----

## **Message Dispatch (Objective-C Runtime)**

A third, less common form of dispatch in Swift is **Message Dispatch**, which is the mechanism used by the Objective-C runtime. It's the **slowest** but most flexible, allowing features like method swizzling (swapping method implementations at runtime).

  * It's used when a method is marked with **`@objc dynamic`**.
  * The system searches the entire class hierarchy at runtime to find the method.

## **Summary Comparison**

| Feature | Static Dispatch | Dynamic Dispatch |
| :--- | :--- | :--- |
| **Resolution Time** | Compile Time | Run Time |
| **Performance** | **Fastest** (Direct jump) | Slower (Runtime lookup) |
| **Flexibility** | Low (No overriding) | **High** (Polymorphism) |
| **Common Use** | Structs, Enums, `final` Classes/Methods | Overridable Class Methods, Protocol Requirements |

