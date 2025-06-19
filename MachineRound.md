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

