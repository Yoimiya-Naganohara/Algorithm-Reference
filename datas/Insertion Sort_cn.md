[English](Insertion%20Sort.md) | [中文](Insertion%20Sort_cn.md)

# 插入排序

插入排序是一种简单的排序算法，它一次构建最终排序的数组（或列表）。 与快速排序、堆排序或归并排序等更高级的算法相比，它在大型列表上的效率要低得多。

## 代码示例 (Python)

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

# 示例用法
arr = [12, 11, 13, 5, 6]
sorted_arr = insertion_sort(arr)
print("排序后的数组是:", sorted_arr)
```

## 代码示例 (Java)

```java
class Main {
    public static void insertionSort(int arr[]) {
        int n = arr.length;
        for (int i = 1; i < n; ++i) {
            int key = arr[i];
            int j = i - 1;

            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }

    public static void main(String args[]) {
        int arr[] = {12, 11, 13, 5, 6};

        insertionSort(arr);

        System.out.println("排序后的数组:");
        for (int i = 0; i < arr.length; ++i)
            System.out.print(arr[i] + " ");

        System.out.println();
    }
}
```

## 代码示例 (C)

```c
#include <stdio.h>

void insertionSort(int arr[], int n) {
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);

    insertionSort(arr, n);

    printf("排序后的数组: \n");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");

    return 0;
}
```

## 代码示例 (C++)

```cpp
#include <iostream>

void insertionSort(int arr[], int n) {
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);

    insertionSort(arr, n);

    std::cout << "排序后的数组: \n";
    for (int i = 0; i < n; i++)
        std::cout << arr[i] << " ";
    std::cout << "\n";

    return 0;
}
```

## 时间复杂度

- 最佳情况：O(n)，当数组已经排序时。
- 平均情况：O(n^2)，当数组元素是随机顺序时。
- 最坏情况：O(n^2)，当数组按相反的顺序排序时。

## 空间复杂度

插入排序的空间复杂度为 O(1)，因为它对元素进行原地排序，不需要大量的额外内存。

## 使用场景

- 适用于小型数据集。
- 当数组已经部分排序时很有用。
- 可用于在线算法，其中数据是连续接收的，需要实时排序。
