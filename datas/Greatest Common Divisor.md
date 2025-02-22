[English](Greatest%20Common%20Divisor.md) | [中文](Greatest%20Common%20Divisor_cn.md)
# Greatest Common Divisor (GCD)

The greatest common divisor (GCD) of two integers is the largest integer that divides both numbers without a remainder.

## Code Example (Python)

```python
def gcd(a, b):
    while(b):
        a, b = b, a % b
    return a

# Example usage
num1 = 60
num2 = 48
print(f"GCD of {num1} and {num2} is {gcd(num1, num2)}")
```

## Code Example (Java)

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
        System.out.println("GCD of " + num1 + " and " + num2 + " is " + gcd(num1, num2));
    }
}
```

## Code Example (C)

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
    printf("GCD of %d and %d is %d\n", num1, num2, gcd(num1, num2));
    return 0;
}
```

## Code Example (C++)

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
    std::cout << "GCD of " << num1 << " and " << num2 << " is " << gcd(num1, num2) << std::endl;
    return 0;
}
```

## Time Complexity

The time complexity of the Euclidean algorithm for finding the GCD is O(log(min(a, b))), where a and b are the two input numbers.

## Use Cases

GCD is used in:
- Simplifying fractions
- Cryptography
- Solving Diophantine equations
