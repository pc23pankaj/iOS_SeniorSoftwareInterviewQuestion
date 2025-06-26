### Q. Can you compare Class vs Structure in Swift using just 4 key points?
**Answer**

## Class vs Structure in Swift

| Feature        | Class                                  | Struct                                  |
|----------------|-----------------------------------------|------------------------------------------|
| **Type**       | Reference type                          | Value type                               |
| **Inheritance**| Supports inheritance                    | Does not support inheritance             |
| **Memory**     | Stored in heap (shared reference)       | Stored in stack (copied on assignment)   |
| **Initializer**| Requires manual initializer             | Gets default memberwise initializer      |


### 🧠 When to Use What?

| Use Class when:                                                   | Use Struct when:                                              |
|-------------------------------------------------------------------|---------------------------------------------------------------|
| You need to inherit from another type.                            | You are modeling simple, independent data.                    |
| You want to share instances across multiple parts of your app.    | You want safety from unintended side effects.                 |
| You need to manage identity (e.g., reference equality using ===). | Performance is a priority and data doesn’t need to be shared. |


### ✅ Code Explanation & Output
### 🧠 Class Example (Reference Type)

```swift 
class StudentClass {
   var name: String
   var grade: Int
   init(name: String, grade: Int) {
      self.name = name
      self.grade = grade
   }
}
let student1 = StudentClass(name: "Ramesh Chandra", grade: 9)
let student2 = student1
student2.name = "Ramesh Kant"
````
student1 and student2 refer to the same memory location.
Changing student2.name also changes student1.name.

```swift 
Output:
student1 name: Ramesh Kant
student2 name: Ramesh Kant
```

### 🧠 Struct Example (Value Type)

```swift 
struct StudentStruct {
   var name: String
   var grade: Int
}
let student3 = StudentStruct(name: "Anish Sharma", grade: 8)
var student4 = student3
student4.name = "Anish Gupta"
```
student3 and student4 are two separate copies.
Changing student4.name does not affect student3.name.

```swift 
Output:
student3 name: Anish Sharma
student4 name: Anish Gupta
student4 grade: 8
```


### Benefits of Struct vs Class in Swift

| Feature             | `struct` (Value Type)                            | `class` (Reference Type)                          |
| ------------------- | ------------------------------------------------ | ------------------------------------------------- |
| **Memory Model**    | Stored on the stack (efficient)                  | Stored on the heap (with reference counting)      |
| **Performance**     | Faster for small/lightweight objects             | Better for complex/shared objects                 |
| **Thread-Safe**     | Yes (copied on assignment → no shared state)     | No (shared state requires synchronization)        |
| **Mutability**      | Immutable by default (`mutating` keyword needed) | Mutable by default                                |
| **Inheritance**     | ❌ Not supported                                  | ✅ Supports single inheritance                     |
| **Use Case**        | Use for data models, value semantics             | Use for objects with identity and shared behavior |
| **ARC Involvement** | ❌ Not managed by ARC                             | ✅ Managed by ARC (Automatic Reference Counting)   |



**✅ What is a Class Function in Swift?**
   - In Swift, a class function is a method that belongs to the class itself (not an instance) and can be overridden by a subclass.
```swift
class Animal {
    class func sound() {
        print("Animal sound")
    }
}

class Dog: Animal {
    override class func sound() {
        print("Bark")
    }
}
```

**✅ What is static function in swift ?**
- A static function in Swift is a type method that belongs to the type itself (not to any instance) and cannot be overridden by subclasses (if used in a class).

```
struct MathUtils {
    static func square(of number: Int) -> Int {
        return number * number
    }
}

// Usage
let result = MathUtils.square(of: 5)
print(result)  // Output: 25
```
```
class MyClass {
    static func greet() {
        print("Hello from MyClass!")
    }
}

// Usage
MyClass.greet()

```
🔁 If you want a method that can be overridden in subclasses, use class func instead of static func.

**Difference between Class Function vs Static Function**
| Feature         | `static func`                                | `class func`                          |
| --------------- | -------------------------------------------- | ------------------------------------- |
| **Overridable** | ❌ Cannot be overridden in subclass           | ✅ Can be overridden in subclass       |
| **Binding**     | Bound at compile time                        | Dynamically dispatched                |
| **Used In**     | Structs, Enums, and Classes                  | Only in Classes                       |
| **Purpose**     | Utility methods that shouldn’t be overridden | Allow polymorphism at the class level |


## 3. Actor (Introduced in Swift 5.5, for concurrency)
**Reference type**
**Thread-safe:** only 1 task accesses an actor’s data at a time
Great for managing state in concurrent environments
Cannot inherit from other classes/actors
```
🔸 Example:
actor Counter {
    var value = 0
    func increment() {
        value += 1
    }
}
```
✅ Use Actor when:
You need to protect mutable state across threads
You want built-in synchronization
You're working with Swift Concurrency

## Actors
| Feature           | `Struct`         | `Class`         | `Actor`          |
| ----------------- | ---------------- | --------------- | ---------------- |
| Type              | Value type       | Reference type  | Reference type   |
| Thread-safe       | ✅ Yes            | ❌ No            | ✅ Yes (isolated) |
| Inheritance       | ❌ No             | ✅ Yes           | ❌ No             |
| Stored in         | Stack            | Heap            | Heap             |
| Memory Management | Automatic (copy) | ARC             | ARC              |
| Use for           | Small models     | Complex objects | Concurrent state |

