Swift offers several types of initializers that serve different purposes in setting up an instance of a class, structure, or enumeration. 🛠️

The three main types are:

-----

## **1. Designated Initializers (The Main Initializer)**

  * **Purpose:** These are the primary initializers for a **class** (structs and enums do not have this distinction). They are responsible for ensuring that all properties introduced by their class are fully initialized.
  * **Role in Inheritance:** If a class has a designated initializer, it must call an initializer from its immediate superclass to complete the initialization of inherited properties.
  * **Syntax:** They are defined simply using the `init(...)` keyword.

<!-- end list -->

```swift
class Vehicle {
    var numberOfWheels: Int
    var color: String

    // Designated Initializer
    init(wheels: Int, color: String) {
        self.numberOfWheels = wheels
        self.color = color
    }
}
```

-----

## **2. Convenience Initializers (Secondary Initializers)**

  * **Purpose:** These are secondary, optional initializers for a **class**. They provide a more convenient way to create an instance for common use cases or with fewer parameters. They often call a designated initializer from the *same class* to do the bulk of the setup.
  * **Rules (Delegation):**
      * A convenience initializer **must** call another initializer from the *same class*.
      * It must ultimately end up calling a designated initializer.
      * It cannot call an initializer from its superclass.
  * **Syntax:** They are defined using the `convenience init(...)` keyword.

<!-- end list -->

```swift
class Car: Vehicle {
    var isSedan: Bool
    
    // Designated Initializer (Must call super.init)
    init(color: String, isSedan: Bool) {
        self.isSedan = isSedan
        super.init(wheels: 4, color: color)
    }

    // Convenience Initializer (Must call self.init)
    convenience init(defaultColor: String) {
        // Delegates to the designated initializer of the same class
        self.init(color: defaultColor, isSedan: true)
    }
}
```

-----

## **3. Failable Initializers (Handling Failure)**

  * **Purpose:** These initializers are used when the initialization of an instance might **fail** for reasons like invalid input data, missing external resources, or a structural requirement that isn't met.
  * **Return Value:** A failable initializer returns an **optional** instance of the type (`Type?`). If initialization succeeds, it returns a valid instance; otherwise, it returns `nil`.
  * **Syntax:** They are defined using `init?()`.

<!-- end list -->

```swift
struct Temperature {
    var celsius: Double
    
    // Failable Initializer
    init?(fahrenheit: Double) {
        // Example of a condition that causes failure
        guard fahrenheit >= -459.67 else { // Absolute zero in Fahrenheit
            return nil
        }
        self.celsius = (fahrenheit - 32.0) / 1.8
    }
}

// Usage:
let freezing = Temperature(fahrenheit: 32.0) // Optional<Temperature>, contains a value
let impossible = Temperature(fahrenheit: -500.0) // Optional<Temperature>, contains nil
```

### **Related Initializer Types**

Besides the main three, Swift also features:

  * **Required Initializers:** Used in classes, these ensure that every subclass implements the initializer. They are defined with the `required` keyword and are often seen when working with protocols that require specific initializers.
  * **Automatic Initializers:** Swift provides a **memberwise initializer** automatically for structs (and optionally for classes without designated initializers) if you don't define any custom initializers yourself. It lets you initialize properties by passing their names as arguments.
      * *Example (Struct):*
        ```swift
        struct Point {
            var x: Int
            var y: Int
        }
        let p = Point(x: 10, y: 20) // Automatically provided
        ```

Would you like a more detailed explanation of the rules for designated and convenience initializers in class inheritance?
