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



