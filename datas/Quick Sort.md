[English](Quick%20Sort.md) | [中文](Quick%20Sort_cn.md)
# Quick Sort

Quicksort is a divide-and-conquer algorithm. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively.

## Code Example (Python)

```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)

# Example usage
arr = [3, 6, 8, 10, 1, 2, 1]
print(quicksort(arr))
```

## Time Complexity

- Best case: O(n log n)
- Average case: O(n log n)
- Worst case: O(n^2)

## Use Cases

Quicksort is often used in practice because it is efficient for large datasets and has good cache performance. It is also a popular choice for sorting algorithms in many programming languages and libraries.
