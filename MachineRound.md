### //Two Sum Problem. Find all the pairs from ana given array which sum is equal to target.
```
let inputArray = [2, 3, 4, 3, 4, 1, 6, 6, 6, 7, 5, 9, 1, 8, 9, 1, 1, 8, 9]
let target = 10


func finalApproach(input: [Int], sum: Int) {
    var sortedArray = input.sorted()
    var left = 0
    var right = sortedArray.count - 1
    
    while (left < right) {
        if left != 0 && sortedArray[left] == sortedArray[left - 1] {
            left = left + 1
            continue
        }
        
        let s = sortedArray[left] + sortedArray[right]
        if s == sum {
            print(" (\(sortedArray[left]), \(sortedArray[right]))")
            left = left + 1
            right = right - 1
        }
        else if s > sum {
            right = right - 1
        }
        else {
            left = left - 1
        }
    }
}

finalApproach(input: inputArray, sum:target)
```


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


print("1. Maximum Element:")
print("   For Loop: \(findMaxUsingLoop(testArray) ?? 0)")
print("   HOF: \(findMaxUsingHOF(testArray) ?? 0)\n")

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

print("2. Sum of Elements:")
print("   For Loop: \(sumUsingLoop(testArray))")
print("   HOF: \(sumUsingHOF(testArray))\n")


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

print("3. Even Numbers:")
print("   For Loop: \(findEvensUsingLoop(testArray))")
print("   HOF: \(findEvensUsingHOF(testArray))\n")


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


print("4. Count Occurrences of 1:")
print("   For Loop: \(countOccurrencesUsingLoop(testArray, target: 1))")
print("   HOF: \(countOccurrencesUsingHOF(testArray, target: 1))\n")

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


print("5. Square All Elements:")
print("   For Loop: \(squareElementsUsingLoop([1, 2, 3, 4]))")
print("   HOF: \(squareElementsUsingHOF([1, 2, 3, 4]))\n")


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

print("6. Has Duplicates:")
print("   For Loop: \(hasDuplicatesUsingLoop(testArray))")
print("   HOF: \(hasDuplicatesUsingHOF(testArray))\n")

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

print("7. Second Largest:")
print("   For Loop: \(findSecondLargestUsingLoop(testArray) ?? 0)")
print("   HOF: \(findSecondLargestUsingHOF(testArray) ?? 0)\n")


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

print("8. Common Elements:")
print("   For Loop: \(findCommonElementsUsingLoop(array1, array2))")
print("   HOF: \(findCommonElementsUsingHOF(array1, array2))\n")

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

print("9. Is Sorted:")
print("   For Loop: \(isSortedUsingLoop([1, 2, 3, 4, 5]))")
print("   HOF: \(isSortedUsingHOF([1, 2, 3, 4, 5]))\n")

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

print("10. Missing Number (1-5):")
print("    For Loop: \(findMissingNumberUsingLoop([1, 2, 4, 5], n: 5) ?? 0)")
print("    HOF: \(findMissingNumberUsingHOF([1, 2, 4, 5], n: 5) ?? 0)")

```

Sure! Here are **two separate Swift programs**: one for checking a **Palindrome number**, and the other for checking an **Armstrong number**.

---

## ✅ 1. **Palindrome Number in Swift**

> A number is a palindrome if it reads the same forwards and backwards.
> Example: `121`, `1331`, `444`

```swift
func isPalindrome(_ number: Int) -> Bool {
    let original = number
    var reversed = 0
    var n = number

    while n > 0 {
        let digit = n % 10
        reversed = reversed * 10 + digit
        n /= 10
    }

    return original == reversed
}

// Example usage:
let num1 = 121
print("\(num1) is palindrome? \(isPalindrome(num1))") // true

let num2 = 123
print("\(num2) is palindrome? \(isPalindrome(num2))") // false
```

---

## ✅ 2. **Armstrong Number in Swift**

> An Armstrong number is one where the sum of each digit raised to the power of the total number of digits equals the number itself.
> Example:
> `153` → $1³ + 5³ + 3³ = 153$

```swift
func isArmstrong(_ number: Int) -> Bool {
    let digits = String(number).compactMap { Int(String($0)) }
    let power = digits.count
    let sum = digits.reduce(0) { $0 + Int(pow(Double($1), Double(power))) }
    return sum == number
}

// Example usage:
let num3 = 153
print("\(num3) is armstrong? \(isArmstrong(num3))") // true

let num4 = 123
print("\(num4) is armstrong? \(isArmstrong(num4))") // false
```

Great! Let’s start with **3 useful Swift interview questions** from the list, complete with **solutions**:

---

## ✅ 3. **Reverse a Number**

```swift
func reverseNumber(_ number: Int) -> Int {
    var num = number
    var reversed = 0

    while num != 0 {
        let digit = num % 10
        reversed = reversed * 10 + digit
        num /= 10
    }

    return reversed
}

// Test
print(reverseNumber(1234)) // Output: 4321
```

---

## ✅ 4. **Check for Prime Number**

```swift
func isPrime(_ number: Int) -> Bool {
    if number <= 1 { return false }
    if number <= 3 { return true }

    for i in 2...Int(sqrt(Double(number))) {
        if number % i == 0 {
            return false
        }
    }
    return true
}

// Test
print(isPrime(7))   // true
print(isPrime(10))  // false
```

---

## ✅ 5. **Sum of Digits of a Number**

```swift
func sumOfDigits(_ number: Int) -> Int {
    var sum = 0
    var num = number

    while num > 0 {
        sum += num % 10
        num /= 10
    }

    return sum
}

// Test
print(sumOfDigits(12345)) // Output: 15
```

---

Perfect! Here's the next set of classic interview questions with Swift implementations:

---

## ✅ 6. **Fibonacci Series (Iterative)**

```swift
func printFibonacciSeries(count: Int) {
    var a = 0, b = 1
    for _ in 0..<count {
        print(a, terminator: " ")
        let next = a + b
        a = b
        b = next
    }
    print()
}

// Test
printFibonacciSeries(count: 10)
// Output: 0 1 1 2 3 5 8 13 21 34
```

---

## ✅ 7. **Perfect Number**

> A **perfect number** is a positive integer that is equal to the sum of its **proper divisors** (excluding itself).
> Example: `28 → 1 + 2 + 4 + 7 + 14 = 28`

```swift
func isPerfect(_ number: Int) -> Bool {
    if number <= 1 { return false }
    var sum = 0
    for i in 1..<number {
        if number % i == 0 {
            sum += i
        }
    }
    return sum == number
}

// Test
print(isPerfect(28))  // true
print(isPerfect(12))  // false
```

---

## ✅ 8. **Strong Number**

> A **strong number** is a number where the sum of the factorials of its digits is equal to the number.
> Example: `145 → 1! + 4! + 5! = 145`

```swift
func factorial(_ n: Int) -> Int {
    return (1...max(1, n)).reduce(1, *)
}

func isStrongNumber(_ number: Int) -> Bool {
    let digits = String(number).compactMap { Int(String($0)) }
    let sum = digits.map { factorial($0) }.reduce(0, +)
    return sum == number
}

// Test
print(isStrongNumber(145)) // true
print(isStrongNumber(123)) // false
```

---

## ✅ 9. **Find the Maximum and Minimum in an Array**

```swift
func findMinMax(_ arr: [Int]) -> (min: Int, max: Int)? {
    guard let first = arr.first else { return nil }
    var minVal = first
    var maxVal = first

    for num in arr {
        if num < minVal { minVal = num }
        if num > maxVal { maxVal = num }
    }

    return (minVal, maxVal)
}

// Test
let numbers = [4, 7, 1, 9, 2]
if let result = findMinMax(numbers) {
    print("Min: \(result.min), Max: \(result.max)")
}
```

---

## ✅ 10. **Remove Duplicates from an Array**

```swift
func removeDuplicates(_ arr: [Int]) -> [Int] {
    var seen = Set<Int>()
    var result: [Int] = []

    for num in arr {
        if !seen.contains(num) {
            result.append(num)
            seen.insert(num)
        }
    }
    return result
}

// Test
print(removeDuplicates([1, 2, 2, 3, 4, 3])) // [1, 2, 3, 4]
```

---

## ✅ 11. **Find All Pairs That Sum to a Target (Two Sum)**

```swift
func findPairsThatSum(to target: Int, in arr: [Int]) -> [(Int, Int)] {
    var result = [(Int, Int)]()
    var seen = Set<Int>()

    for num in arr {
        let complement = target - num
        if seen.contains(complement) {
            result.append((complement, num))
        }
        seen.insert(num)
    }
    return result
}

// Test
print(findPairsThatSum(to: 10, in: [2, 3, 7, 5, 8, 1, 9])) // [(3,7), (5,5), (1,9)]
```

---

## ✅ 12. **Transpose a Matrix**

> Convert rows to columns and vice versa.

```swift
func transpose(matrix: [[Int]]) -> [[Int]] {
    guard !matrix.isEmpty else { return [] }

    let rows = matrix.count
    let cols = matrix[0].count
    var result = Array(repeating: Array(repeating: 0, count: rows), count: cols)

    for i in 0..<rows {
        for j in 0..<cols {
            result[j][i] = matrix[i][j]
        }
    }
    return result
}

// Test
let matrix = [[1, 2, 3], [4, 5, 6]]
print(transpose(matrix: matrix)) // [[1,4], [2,5], [3,6]]
```

---

## ✅ 13. **Print Diagonal Elements of a Square Matrix**

```swift
func printDiagonals(matrix: [[Int]]) {
    let n = matrix.count
    var primary = [Int]()
    var secondary = [Int]()

    for i in 0..<n {
        primary.append(matrix[i][i])
        secondary.append(matrix[i][n - i - 1])
    }

    print("Primary diagonal: \(primary)")
    print("Secondary diagonal: \(secondary)")
}

// Test
let square = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
printDiagonals(matrix: square)
```

---

### ✅ 1. **Right-Angled Triangle**

```
*
**
***
****
*****
```

```swift
func rightAngledTriangle(rows: Int) {
    for i in 1...rows {
        for _ in 1...i {
            print("*", terminator: "")
        }
        print()
    }
}

rightAngledTriangle(rows: 5)
```

---

### ✅ 2. **Inverted Triangle**

```
*****
****
***
**
*
```

```swift
func invertedTriangle(rows: Int) {
    for i in stride(from: rows, to: 0, by: -1) {
        for _ in 1...i {
            print("*", terminator: "")
        }
        print()
    }
}

invertedTriangle(rows: 5)
```

---

### ✅ 3. **Right-Aligned Triangle**

```
    *
   **
  ***
 ****
*****
```

```swift
func rightAlignedTriangle(rows: Int) {
    for i in 1...rows {
        for _ in 0..<(rows - i) {
            print(" ", terminator: "")
        }
        for _ in 1...i {
            print("*", terminator: "")
        }
        print()
    }
}

rightAlignedTriangle(rows: 5)
```

---

### ✅ 4. **Pyramid Pattern**

```
    *
   ***
  *****
 *******
*********
```

```swift
func pyramid(rows: Int) {
    for i in 1...rows {
        for _ in 1...(rows - i) {
            print(" ", terminator: "")
        }
        for _ in 1...(2 * i - 1) {
            print("*", terminator: "")
        }
        print()
    }
}

pyramid(rows: 5)
```

---

### ✅ 5. **Diamond Pattern**

```
    *
   ***
  *****
   ***
    *
```

```swift
func diamond(rows: Int) {
    // Top half
    for i in 1...rows {
        for _ in 1...(rows - i) {
            print(" ", terminator: "")
        }
        for _ in 1...(2 * i - 1) {
            print("*", terminator: "")
        }
        print()
    }
    // Bottom half
    for i in stride(from: rows - 1, to: 0, by: -1) {
        for _ in 1...(rows - i) {
            print(" ", terminator: "")
        }
        for _ in 1...(2 * i - 1) {
            print("*", terminator: "")
        }
        print()
    }
}

diamond(rows: 3)
```

---


