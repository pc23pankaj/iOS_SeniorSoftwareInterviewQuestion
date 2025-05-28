# 🎯 High-Order Functions in Swift

## 📘 What is a High-Order Function?
A **high-order function** is a function that either:
- Takes another function as an argument, **or**
- Returns another function.

Swift provides several built-in high-order functions that work on collections like arrays, such as `map`, `filter`, `reduce`, `sorted`, and `flatMap`.

---



## 🔢 `sorted`

### Description:
Returns a new array with the elements sorted in ascending order.  
The array’s elements must conform to the `Comparable` protocol.

```swift
let numbers = [6, 2, 9, 1]
let ascending = numbers.sorted()           // [1, 2, 6, 9]
let descending = numbers.sorted(by: >)     // [9, 6, 2, 1]
```
>Or using a closure:

```
let descending = numbers.sorted { a, b in a > b }
```



## 🔁 map

### Description:
Transforms each element in a collection and returns a new array with the transformed values.

```
let numbers = [1, 2, 3]
let numbersAsString = numbers.map { String($0) }  // ["1", "2", "3"]
```



## 🧼 compactMap

### Description:

- compactMap is used to:
    Transform elements like map
    Remove any nil values in the process

It’s great when mapping optional values and you want to automatically skip nils.

>**Syntax:**

```
let strings = ["1", "two", "3", "four"]
let numbers = strings.compactMap { Int($0) } // [1, 3]
```
"1" and "3" are converted to Int
"two" and "four" return nil → compactMap excludes them

>**Key Difference vs map:**

map will keep the optional results: [Optional(1), nil, Optional(3), nil]
compactMap removes nils and returns [1, 3]



## 🔀 flatMap

### Description:
Combines the functionality of map and flattening nested collections into a single array.
```
let nested = [[1, 2], [3, 4], [5, 6]]
let flattened = nested.flatMap { $0 }    // [1, 2, 3, 4, 5, 6]
```
Useful when working with optional values or arrays of arrays.



## 🔎 filter

### Description:
Returns a new array containing only the elements that satisfy a given condition.
```
let numbers = [1, 3, 2, 0, 6, 8, 5, 9]
let filtered = numbers.filter { $0 < 5 }          // [1, 3, 2, 0]
```
> Or using an explicit closure:
```
let filtered = numbers.filter { (a) -> Bool in return a < 5 }
```



## 🧮 reduce

### Description:
- Combines all elements in a collection into a single value.

>**Example – Sum:**
```
let numbers = [1, 2, 3, 4]
let sum = numbers.reduce(0) { $0 + $1 }           // 10
```
>**Example – Convert to String:**

```
let numbers = [1, 2, 3]
let resultString = numbers.reduce("") { $0 + String($1) } // "123"
```
>**Or with full closure syntax:**

```
let resultString = numbers.reduce("") { (result, a) -> String in
    return result + String(a)
  }
```

## ✅ Summary Table


| Function     | Purpose                                        | Returns                |
| ------------ | ---------------------------------------------- | ---------------------- |
| `sorted`     | Sort elements (ascending or with custom logic) | New sorted array       |
| `map`        | Transform each element                         | New array              |
| `compactMap` | Transform + remove nil values                  | New non-optional array |
| `flatMap`    | Map + Flatten nested collections               | Flattened array        |
| `filter`     | Keep elements that match a condition           | Filtered array         |
| `reduce`     | Combine all elements into a single value       | One value              |





