[English](Primality%20Test.md) | [中文](Primality%20Test_cn.md)
# Primality Test

A primality test is an algorithm for determining whether an input number is prime. Unlike prime factorization, primality tests do not generally give the prime factors, only stating whether the input number is prime or not.

## Code Example (Python)

```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

# Example usage
number = 29
if is_prime(number):
    print(f"{number} is a prime number")
else:
    print(f"{number} is not a prime number")
```

## Code Example (Java)

```java
class Main {
  static boolean isPrime(int n) {
    if (n <= 1)
      return false;
    for (int i = 2; i <= Math.sqrt(n); i++) {
      if (n % i == 0)
        return false;
    }
    return true;
  }

  public static void main(String[] args) {
    int number = 29;
    if (isPrime(number))
      System.out.println(number + " is a prime number");
    else
      System.out.println(number + " is not a prime number");
  }
}
```

## Code Example (C)

```c
#include <stdio.h>
#include <stdbool.h>
#include <math.h>

bool isPrime(int n) {
    if (n <= 1)
        return false;
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

int main() {
    int number = 29;
    if (isPrime(number))
        printf("%d is a prime number\n", number);
    else
        printf("%d is not a prime number\n", number);
    return 0;
}
```

## Code Example (C++)

```cpp
#include <iostream>
#include <cmath>

bool isPrime(int n) {
    if (n <= 1)
        return false;
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

int main() {
    int number = 29;
    if (isPrime(number))
        std::cout << number << " is a prime number" << std::endl;
    else
        std::cout << number << " is not a prime number" << std::endl;
    return 0;
}
```

## Time Complexity

The time complexity of this primality test is O(sqrt(n)), where n is the number being tested.

## Use Cases

Primality tests are used in:
- Cryptography (e.g., generating RSA keys)
- Number theory research
- Testing the correctness of other algorithms
