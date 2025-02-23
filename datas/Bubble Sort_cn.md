[English](Bubble%20Sort.md) | [中文](Bubble%20Sort_cn.md)

# 冒泡排序

冒泡排序是一种简单的排序算法，它重复遍历列表，比较相邻元素并交换它们，如果它们的顺序错误。 重复传递列表，直到不需要交换，这表明列表已排序。

## 代码示例 (Python)

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
    return arr

# 示例用法
arr = [64, 34, 25, 12, 22, 11, 90]
sorted_arr = bubble_sort(arr)
print("排序后的数组是:", sorted_arr)
```

## 代码示例 (Java)

```java
class Main {
    static void bubbleSort(int arr[]) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++)
            for (int j = 0; j < n - i - 1; j++)
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
    }

    public static void main(String args[]) {
        int arr[] = {64, 34, 25, 12, 22, 11, 90};
        bubbleSort(arr);
        System.out.println("排序后的数组");
        for (int i = 0; i < arr.length; ++i)
            System.out.print(arr[i] + " ");
        System.out.println();
    }
}
```

## 代码示例 (C)

```c
#include <stdio.h>

void bubbleSort(int arr[], int n) {
    int i, j;
    for (i = 0; i < n - 1; i++)
        for (j = 0; j < n - i - 1; j++)
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j