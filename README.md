# iOS_SeniorSoftwareInterviewQuestion
This repository contains a collection of Swift interview questions that cover various essential concepts for iOS developers. These questions range from basic to advanced topics, making it an ideal resource for preparing for iOS interviews that focus on Swift.


## 1. **What is Protocol ?**
 **Answer :**
- Protocols are used to define a “blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality.”
- It’s an Interface 
- Protocols help your class and structure to adhere to a certain set of disciplines

## 2. **What is Closures ?**
 **Answer :**
Closures are self-contained blocks of functionality that can be passed around and used in your code. Closures in Swift are similar to blocks in C and Objective-C and lambdas in other programming languages.

Syntax of closure
let greeting = { (name: String) -> String in
    return "Hello, \(name)!"
}

## 3. Type of closure?**
**Answer :**
Based on Capturing Strategy
</br> - Escaping Closures (@escaping):</br> Stored and executed after the function returns (e.g., for completion handlers).
</br> - Non-Escaping Closures:</br> Executed within the function before it returns (default behavior). It is also a default closure in Swift bcoz in this swift don’t need to allocate memory for that so non escaping closure will execute then and there, If we calling API or doing database related activity then use @escaping closure else it is by default NonEscaping closure.
</br> - Autoclosures (@autoclosure):</br> Automatically wraps an expression in a closure. Mostly used for syntactic sugar (e.g., assert(condition)).

## 4. Why [weak self] is used in closure?**
**Answer :**
[weak self] is a capture list used in closures to avoid strong reference cycles (retain cycles), especially when referencing self inside the closure.

Syntax for denoting [weak self]:

someFunctionWithClosure { [weak self] in
    self?.doSomething()
}

What it does:
- [weak self] makes self a weak reference inside the closure.
- It becomes an optional (self?), so you need to safely unwrap it before using it.


## 5. What is a Trailing Closure in Swift? And how it is different from normal closure**
**Answer :**
A trailing closure is a special syntax that allows you to write a closure outside of the parentheses if it's the last argument to a function.

- Let suppose we a function name 'perform' is a function that takes a closure as a parameter. The closure is named action and action takes no parameters and returns nothing (Void). Inside perform, the closure is called using action().
  
func perform(action: () -> Void) {
    action()
}

</br> - Calling the Function (Normal Closure Syntax): </br> 
perform(action: {
    print("Doing something")
})

</br> - Using Trailing Closure Syntax:: </br> 
perform({
    print("Doing something")
})

</br> Summary  </br> 
() -> Void means a closure that takes no parameters and returns nothing.
You can pass inline closure code to a function like perform.
If the closure is the last or only parameter, you can use trailing closure syntax to improve readability.


## 5. What is typeAlais?**
**Answer :**
typealias in Swift is used to define a new name (an alias) for an existing type. It makes code more readable, reusable, and clean, especially when dealing with complex types.

🔹 When to Use:
When a function type or closure type is used in multiple places.
To avoid writing the same complex type over and over again.
To improve code maintainability.

typealias CompletionHandler = (Bool, String) -> Void

🔹 Syntax:
typealias CompletionHandler = (Bool, String) -> Void
Now you can use CompletionHandler instead of repeating the full closure type:
func fetchData(completion: CompletionHandler) {
    // ...
}

🔹 Example with Explanation:

❌ Without typealias:
func downloadFile(completion: (Bool, String) -> Void) {
    completion(true, "Success")
}

✅ With typealias:
typealias DownloadCompletion = (Bool, String) -> Void

func downloadFile(completion: DownloadCompletion) {
    completion(true, "Success")
}












