[English](Binary%20Search.md) | [中文](Binary%20Search_cn.md)
# Binary Search

Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing in half the portion of the list that could contain the item, until you've narrowed down the possible locations to just one.

## Code Example (Python)

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# Example usage
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
target = 7
result = binary_search(arr, target)
print(f"Element found at index: {result}")
```

## Code Example (Java)

```java
class Main {
    static int binarySearch(int arr[], int target) {
        int left = 0, right = arr.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (arr[mid] == target)
                return mid;
            if (arr[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }
        return -1;
    }

    public static void main(String args[]) {
        int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int target = 7;
        int result = binarySearch(arr, target);
        System.out.println("Element found at index: " + result);
    }
}
```

## Code Example (C)

```c
#include <stdio.h>

int binarySearch(int arr[], int target, int left, int right) {
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target)
            return mid;
        if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int target = 7;
    int n = sizeof(arr) / sizeof(arr[0]);
    int result = binarySearch(arr, target, 0, n - 1);
    printf("Element found at index: %d\n", result);
    return 0;
}
```

## Code Example (C++)

```cpp
#include <iostream>

int binarySearch(int arr[], int target, int left, int right) {
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target)
            return mid;
        if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }
    return -1;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int target = 7;
    int n = sizeof(arr) / sizeof(arr[0]);
    int result = binarySearch(arr, target, 0, n - 1);
    std::cout << "Element found at index: " << result << std::endl;
    return 0;
}
```

## Time Complexity

The time complexity of binary search is O(log n), where n is the number of elements in the list. This is because the algorithm divides the search interval in half with each iteration.

## Space Complexity

The space complexity of binary search is O(1) because it uses a constant amount of extra memory, regardless of the size of the input array.

## Use Cases

Binary search is commonly used in:
- Searching in a sorted array or list
- Efficiently finding elements in large datasets
- Implementing search algorithms in databases
- Solving algorithmic problems that require searching in sorted data
