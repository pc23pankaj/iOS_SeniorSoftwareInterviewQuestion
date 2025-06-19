## Q. Short an array and remove duplicates from it?

```
func bubbleSortUnique(_ arr: [Int]) -> [Int] {
    var sortedArr = arr
    let n = sortedArr.count

    for i in 0..<n {
        for j in 0..<n - i - 1 {
            if sortedArr[j] > sortedArr[j + 1] {
                let temp = sortedArr[j]
                sortedArr[j] = sortedArr[j + 1]
                sortedArr[j + 1] = temp
            }
        }
    }

    // Remove duplicates after sorting
    var uniqueArr: [Int] = []
    for num in sortedArr {
        if uniqueArr.last != num {
            uniqueArr.append(num)
        }
    }

    return uniqueArr
}
```
let arr = [2, 6, 3, 4, 8, 9, 5, 6]
let sortedUnique = bubbleSortUnique(arr)
print(sortedUnique) // [2, 3, 4, 5, 6, 8, 9]


import Foundation

let testArray = [3, 1, 4, 1, 5, 9, 2, 6]
let array1 = [1, 2, 3, 4, 5]
let array2 = [3, 4, 5, 6, 7]

print("Test Array: \(testArray)")
print("Array 1: \(array1)")
print("Array 2: \(array2)\n")

// MARK: - 1. Find Maximum Element in Array
```
// Using For Loop
func findMaxUsingLoop(_ array: [Int]) -> Int? {
    guard !array.isEmpty else { return nil }
    
    var maxElement = array[0]
    for i in 1..<array.count {
        if array[i] > maxElement {
            maxElement = array[i]
        }
    }
    return maxElement
}

// Using Higher-Order Function
func findMaxUsingHOF(_ array: [Int]) -> Int? {
    return array.max()
}
```
// MARK: - 2. Find Sum of All Elements
```
// Using For Loop
func sumUsingLoop(_ array: [Int]) -> Int {
    var sum = 0
    for element in array {
        sum += element
    }
    return sum
}

// Using Higher-Order Function
func sumUsingHOF(_ array: [Int]) -> Int {
    return array.reduce(0, +)
}
```
// MARK: - 3. Find Even Numbers
```
// Using For Loop
func findEvensUsingLoop(_ array: [Int]) -> [Int] {
    var evens: [Int] = []
    for number in array {
        if number % 2 == 0 {
            evens.append(number)
        }
    }
    return evens
}

// Using Higher-Order Function
func findEvensUsingHOF(_ array: [Int]) -> [Int] {
    return array.filter { $0 % 2 == 0 }
}
```
// MARK: - 4. Count Occurrences of Element
```
// Using For Loop
func countOccurrencesUsingLoop(_ array: [Int], target: Int) -> Int {
    var count = 0
    for element in array {
        if element == target {
            count += 1
        }
    }
    return count
}

// Using Higher-Order Function
func countOccurrencesUsingHOF(_ array: [Int], target: Int) -> Int {
    return array.filter { $0 == target }.count
}
```
// MARK: - 5. Square All Elements
```
// Using For Loop
func squareElementsUsingLoop(_ array: [Int]) -> [Int] {
    var squared: [Int] = []
    for element in array {
        squared.append(element * element)
    }
    return squared
}

// Using Higher-Order Function
func squareElementsUsingHOF(_ array: [Int]) -> [Int] {
    return array.map { $0 * $0 }
}
```
// MARK: - 6. Check if Array Contains Duplicates
```
// Using For Loop
func hasDuplicatesUsingLoop(_ array: [Int]) -> Bool {
    for i in 0..<array.count {
        for j in (i + 1)..<array.count {
            if array[i] == array[j] {
                return true
            }
        }
    }
    return false
}

// Using Higher-Order Function
func hasDuplicatesUsingHOF(_ array: [Int]) -> Bool {
    return Set(array).count != array.count
}
```

// MARK: - 7. Find Second Largest Element

```
// Using For Loop
func findSecondLargestUsingLoop(_ array: [Int]) -> Int? {
    guard array.count >= 2 else { return nil }
    
    var largest = Int.min
    var secondLargest = Int.min
    
    for element in array {
        if element > largest {
            secondLargest = largest
            largest = element
        } else if element > secondLargest && element != largest {
            secondLargest = element
        }
    }
    
    return secondLargest == Int.min ? nil : secondLargest
}

// Using Higher-Order Function
func findSecondLargestUsingHOF(_ array: [Int]) -> Int? {
    let uniqueSorted = Array(Set(array)).sorted(by: >)
    return uniqueSorted.count >= 2 ? uniqueSorted[1] : nil
}
```

// MARK: - 8. Find Common Elements Between Two Arrays

```
// Using For Loop
func findCommonElementsUsingLoop(_ array1: [Int], _ array2: [Int]) -> [Int] {
    var common: [Int] = []
    for element1 in array1 {
        for element2 in array2 {
            if element1 == element2 && !common.contains(element1) {
                common.append(element1)
            }
        }
    }
    return common
}

// Using Higher-Order Function
func findCommonElementsUsingHOF(_ array1: [Int], _ array2: [Int]) -> [Int] {
    let set2 = Set(array2)
    return Array(Set(array1.filter { set2.contains($0) }))
}
```

// MARK: - 9. Check if Array is Sorted

```
// Using For Loop
func isSortedUsingLoop(_ array: [Int]) -> Bool {
    for i in 1..<array.count {
        if array[i] < array[i - 1] {
            return false
        }
    }
    return true
}

// Using Higher-Order Function
func isSortedUsingHOF(_ array: [Int]) -> Bool {
    return array == array.sorted()
}
```

// MARK: - 10. Find Missing Number (1 to n)

```
// Using For Loop
func findMissingNumberUsingLoop(_ array: [Int], n: Int) -> Int? {
    var present = Array(repeating: false, count: n + 1)
    
    for number in array {
        if number >= 1 && number <= n {
            present[number] = true
        }
    }
    
    for i in 1...n {
        if !present[i] {
            return i
        }
    }
    return nil
}

// Using Higher-Order Function
func findMissingNumberUsingHOF(_ array: [Int], n: Int) -> Int? {
    let expectedSum = n * (n + 1) / 2
    let actualSum = array.reduce(0, +)
    let missing = expectedSum - actualSum
    return missing > 0 ? missing : nil
}

```
// MARK: - Test Cases

print("=== Array Interview Questions Solutions ===\n")


print("1. Maximum Element:")
print("   For Loop: \(findMaxUsingLoop(testArray) ?? 0)")
print("   HOF: \(findMaxUsingHOF(testArray) ?? 0)\n")

print("2. Sum of Elements:")
print("   For Loop: \(sumUsingLoop(testArray))")
print("   HOF: \(sumUsingHOF(testArray))\n")

print("3. Even Numbers:")
print("   For Loop: \(findEvensUsingLoop(testArray))")
print("   HOF: \(findEvensUsingHOF(testArray))\n")

print("4. Count Occurrences of 1:")
print("   For Loop: \(countOccurrencesUsingLoop(testArray, target: 1))")
print("   HOF: \(countOccurrencesUsingHOF(testArray, target: 1))\n")

print("5. Square All Elements:")
print("   For Loop: \(squareElementsUsingLoop([1, 2, 3, 4]))")
print("   HOF: \(squareElementsUsingHOF([1, 2, 3, 4]))\n")

print("6. Has Duplicates:")
print("   For Loop: \(hasDuplicatesUsingLoop(testArray))")
print("   HOF: \(hasDuplicatesUsingHOF(testArray))\n")

print("7. Second Largest:")
print("   For Loop: \(findSecondLargestUsingLoop(testArray) ?? 0)")
print("   HOF: \(findSecondLargestUsingHOF(testArray) ?? 0)\n")

print("8. Common Elements:")
print("   For Loop: \(findCommonElementsUsingLoop(array1, array2))")
print("   HOF: \(findCommonElementsUsingHOF(array1, array2))\n")

print("9. Is Sorted:")
print("   For Loop: \(isSortedUsingLoop([1, 2, 3, 4, 5]))")
print("   HOF: \(isSortedUsingHOF([1, 2, 3, 4, 5]))\n")

print("10. Missing Number (1-5):")
print("    For Loop: \(findMissingNumberUsingLoop([1, 2, 4, 5], n: 5) ?? 0)")
print("    HOF: \(findMissingNumberUsingHOF([1, 2, 4, 5], n: 5) ?? 0)")
