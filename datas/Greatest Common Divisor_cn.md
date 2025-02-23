[English](Greatest%20Common%20Divisor.md) | [中文](Greatest%20Common%20Divisor_cn.md)

# 最大公约数 (GCD)

两个整数的最大公约数 (GCD) 是能同时整除这两个数的最大整数，没有余数。

## 代码示例 (Python)

```python
def gcd(a, b):
    while(b):
        a, b = b, a % b
    return a

# 示例用法
num1 = 60
num2 = 48
print(f"{num1} 和 {num2} 的最大公约数是 {gcd(num1, num2)}")
```

## 代码示例 (Java)

```java
class Main {
    static int gcd(int a, int b) {
        while (b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    public static void main(String[] args) {
        int num1 = 60, num2 = 48;
        System.out.println(num1 + " 和 " + num2 + " 的最大公约数是 " + gcd(num1, num2));
    }
}
```

## 代码示例 (C)

```c
#include <stdio.h>

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    int num1 = 60, num2 = 48;
    printf("%d 和 %d 的最大公约数是 %d\n", num1, num2, gcd(num1, num2));
    return 0;
}
```

## 代码示例 (C++)

```cpp
#include <iostream>

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    int num1 = 60, num2 = 48;
    std::cout << num1 << " 和 " << num2 << " 的最大公约数是 " << gcd(num1, num2) << std::endl;
    return 0;
}
```

## 时间复杂度

用于查找 GCD 的欧几里得算法的时间复杂度为 O(log(min(a, b)))，其中 a 和 b 是两个输入数字。

## 使用场景

GCD 用于：

*   简化分数
*   密码学
*   求解丢番图方程
