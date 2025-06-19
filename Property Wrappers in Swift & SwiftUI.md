## **📦 Property Wrappers in Swift & SwiftUI**

## **🔹 1. What is a Property Wrapper in Swift?**

- A property wrapper is a generic structure that encapsulates read and write access to a property and adds additional behavior to it.
- They are used to reduce boilerplate and reuse logic by wrapping property behavior in a reusable type.
```
@propertyWrapper
struct Capitalized {
    private var value: String = ""

    var wrappedValue: String {
        get { value }
        set { value = newValue.capitalized }
    }

    var projectedValue: String {
        return value.uppercased()
    }
}

struct Person {
    @Capitalized var name: String
}

var p = Person(name: "john doe")
print(p.name)         // John Doe
print(p.$name)        // JOHN DOE

```
- The use of **get** and **set** in a property wrapper is essential because it defines how Swift should:
- Retrieve the value of your property (get)
- Assign a new value to your property (set)


## **🔹 2. What is a Property Wrapper in SwiftUI?**

- SwiftUI heavily uses property wrappers to manage data flow, state, and bindings between views.
##
📘 Notes:
- ✅ Owns data: This property wrapper is responsible for storing its own data.
- ❌ Does not own data: This wrapper accesses or observes data owned elsewhere.

##
| Property Wrapper                | Description                                                                                 | Owns Data |
| ------------------------------- | ------------------------------------------------------------------------------------------- | --------- |
| `@AppStorage`                   | Reads/writes values from `UserDefaults`.                                                    | ✅ Yes     |
| `@Binding`                      | Refers to value type data owned by a different view. Changing it updates the original data. | ❌ No      |
| `@State`                        | Stores local, small amounts of value type data within a view.                               | ✅ Yes     |
| `@Environment`                  | Reads data from the system (e.g. color scheme, accessibility) or custom keys.               | ❌ No      |
| `@EnvironmentObject`            | Reads shared objects injected into the environment.                                         | ❌ No      |
| `@FetchRequest`                 | Starts a Core Data fetch request for a particular entity.                                   | ✅ Yes     |
| `@FocusedBinding`               | Watches values in the key window, e.g., selected text fields.                               | ❌ No      |
| `@FocusedValue`                 | A simpler version of `@FocusedBinding` without automatic unwrapping.                        | ❌ No      |
| `@GestureState`                 | Temporarily stores values for gestures in progress, auto-resets when gesture ends.          | ✅ Yes     |
| `@Namespace`                    | Used for matched geometry effects and animations.                                           | ✅ Yes     |
| `@NSApplicationDelegateAdaptor` | Registers a macOS app delegate class.                                                       | ✅ Yes     |
| `@ObservedObject`               | Refers to an external `ObservableObject` instance.                                          | ❌ No      |
| `@Published`                    | Marks properties inside an `ObservableObject` to notify views when values change.           | ✅ Yes     |
| `@ScaledMetric`                 | Scales numbers based on the user’s Dynamic Type setting.                                    | ✅ Yes     |
| `@SceneStorage`                 | Saves/restores small data amounts for state restoration.                                    | ✅ Yes     |
| `@StateObject`                  | Stores **new** instances of reference types conforming to `ObservableObject`.               | ✅ Yes     |
| `@UIApplicationDelegateAdaptor` | Registers an app delegate class for iOS apps.                                               | ✅ Yes     |

##
