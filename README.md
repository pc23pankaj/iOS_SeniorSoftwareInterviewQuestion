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



## 6. Steps for Notification integration in iOS app from start to end step wise and also explain what are the steps to integrate Image Notifications in Swift?**
💡 **Tip:** _Part 3: Backend Integration interviewer may ask this question so please remember to mention this also._
**Answer :**
Here’s a complete, step-by-step guide to integrating Push Notifications in an iOS app — from start to end, including support for Image Notifications (Rich Notifications) in Swift.
✅ Part 1: Apple Developer Portal Setup

🔹 Step 1: Enable Push Notification Capability
Go to Apple Developer Account.
Navigate to Certificates, IDs & Profiles > Identifiers.
Select your App ID or create a new one.
Enable Push Notifications under "Capabilities".
🔹 Step 2: Create an APNs Key (.p8 File)
Go to Keys > Create Key.
Name it (e.g., "Push Key"), check Apple Push Notifications service (APNs).
Download the .p8 file. Save your:
Key ID
Team ID
Bundle ID
✅ Part 2: Xcode Setup

🔹 Step 3: Enable Push Notification Capability
Open your .xcodeproj or .xcworkspace.
Go to Signing & Capabilities tab.
Add Push Notifications.
(Optional) Add Background Modes > check Remote notifications.

🔹 Step 4: Request Notification Permission
In AppDelegate.swift (or your custom App Delegate in SwiftUI):

import UserNotifications

func registerForPushNotifications() {
    UNUserNotificationCenter.current().delegate = self
    UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { granted, error in
        guard granted else { return }
        DispatchQueue.main.async {
            UIApplication.shared.registerForRemoteNotifications()
        }
    }
}
Then call registerForPushNotifications() in:
func application(_ application: UIApplication, didFinishLaunchingWithOptions...) -> Bool {
    registerForPushNotifications()
    return true
}

🔹 Step 5: Handle Device Token
func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    let tokenParts = deviceToken.map { data in String(format: "%02.2hhx", data) }
    let token = tokenParts.joined()
    print("Device Token: \(token)")
    // Send to your backend server
}

✅ Part 3: Backend Integration (Server Side)

Your backend will use:
.p8 file
Key ID
Team ID
Bundle ID
To send push using APNs token-based authentication (e.g., via Firebase, Node.js with node-apn, or Python with PyAPNs2).

✅ Part 4: Rich Notification with Image (Service Extension)

🔹 Step 6: Create Notification Service Extension
In Xcode, go to:
File > New > Target > Notification Service Extension
Name it (e.g., NotificationService).
In the generated NotificationService.swift:

import UserNotifications

class NotificationService: UNNotificationServiceExtension {

    var contentHandler: ((UNNotificationContent) -> Void)?
    var bestAttemptContent: UNMutableNotificationContent?

    override func didReceive(
        _ request: UNNotificationRequest,
        withContentHandler contentHandler: @escaping (UNNotificationContent) -> Void
    ) {
        self.contentHandler = contentHandler
        bestAttemptContent = (request.content.mutableCopy() as? UNMutableNotificationContent)
        
        guard
            let bestAttemptContent = bestAttemptContent,
            let attachmentURLString = bestAttemptContent.userInfo["image"] as? String,
            let attachmentURL = URL(string: attachmentURLString)
        else {
            contentHandler(request.content)
            return
        }

        downloadImage(from: attachmentURL) { attachment in
            if let attachment = attachment {
                bestAttemptContent.attachments = [attachment]
            }
            contentHandler(bestAttemptContent)
        }
    }

    override func serviceExtensionTimeWillExpire() {
        if let contentHandler = contentHandler, let bestAttemptContent = bestAttemptContent {
            contentHandler(bestAttemptContent)
        }
    }

    private func downloadImage(from url: URL, completion: @escaping (UNNotificationAttachment?) -> Void) {
        URLSession.shared.downloadTask(with: url) { location, _, _ in
            guard let location = location else {
                completion(nil)
                return
            }

            let tmpDir = URL(fileURLWithPath: NSTemporaryDirectory())
            let tmpFile = tmpDir.appendingPathComponent(url.lastPathComponent)

            try? FileManager.default.moveItem(at: location, to: tmpFile)

            let attachment = try? UNNotificationAttachment(identifier: "image", url: tmpFile, options: nil)
            completion(attachment)
        }.resume()
    }
}
Step 7: Send Notification with Image Payload
Your push notification JSON (APNs payload or via FCM) should include the image key in userInfo, like:
{
  "aps": {
    "alert": {
      "title": "New Photo",
      "body": "Check out this image!"
    },
    "sound": "default"
  },
  "image": "https://example.com/path/to/image.jpg"
}

✅ Ensure the URL points to a publicly accessible image, or it won't load.

✅ Final Checks

Make sure your Notification Extension target is added to the scheme.
Test push using:
Postman
Firebase Cloud Messaging
Your backend service
_Use a real device — push notifications don't work in Simulator._



**7. what is dependency Injection in swift and how we can achieve this in simple steps?**
**Answer.**
Dependency Injection (DI) is a design pattern used to provide objects (dependencies) that a class needs, rather than creating them inside the class itself.
🚀 Why Use Dependency Injection?
✅ Improves testability (e.g., mock dependencies in unit tests)
✅ Promotes loose coupling between components
✅ Increases flexibility and maintainability
✅ What is Dependency?

A dependency is any object a class relies on to function.
Example:
class Engine {
    func start() {
        print("Engine started")
    }
}

class Car {
    let engine = Engine() // tightly coupled
}
Here, Car creates its own dependency — not ideal.
✅ What is Dependency Injection?

Instead of creating the dependency, we inject it:
class Car {
    let engine: Engine
    init(engine: Engine) { // Dependency Injection
        self.engine = engine
    }
}
Now Car does not create the engine; it just uses one that is passed to it.
🔧 Types of Dependency Injection in Swift

Type	How It Works	Example Use
1. Initializer Injection	Passed in constructor (init)	✅ Preferred
2. Property Injection	Assigned after initialization	Optional
3. Method Injection	Passed as method parameters	Limited use
🔹 1. Initializer Injection (Recommended)
class Logger {
    func log(_ message: String) {
        print("LOG:", message)
    }
}

class NetworkManager {
    let logger: Logger
    init(logger: Logger) {
        self.logger = logger
    }
    func fetchData() {
        logger.log("Fetching data...")
    }
}

// Inject the dependency
let logger = Logger()
let networkManager = NetworkManager(logger: logger)
networkManager.fetchData()
🔹 2. Property Injection
class Service {
    func run() { print("Service running") }
}

class Controller {
    var service: Service? // Inject after init
}

let controller = Controller()
controller.service = Service()
controller.service?.run()
🔹 3. Method Injection
class Analytics {
    func track(event: String) {
        print("Tracked:", event)
    }
}

func performLogin(analytics: Analytics) {
    // Injected only for this method
    analytics.track(event: "UserLoggedIn")
}
🔄 Bonus: Using Protocols for Better Testability

protocol EngineProtocol {
    func start()
}

class Engine: EngineProtocol {
    func start() { print("Real Engine started") }
}

class MockEngine: EngineProtocol {
    func start() { print("Mock Engine started (test)") }
}

class Car {
    let engine: EngineProtocol

    init(engine: EngineProtocol) {
        self.engine = engine
    }
}
Now you can inject MockEngine() for unit tests.

✅ Summary

- Testability Inject mocks/fakes
- Decoupling No hardcoded dependencies
- Flexibility Easy to swap components
- Clean Architecture Supports SOLID principles


