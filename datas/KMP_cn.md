[English](KMP.md) | [中文](KMP_cn.md)

# Knuth-Morris-Pratt (KMP) 算法

KMP 算法是一种字符串搜索算法，它通过观察到当不匹配发生时，要搜索的“词”本身就包含了足够的信息来确定下一次匹配可能开始的位置，从而避免了对先前匹配字符的重新检查，以此在主“文本字符串”S中搜索“词”W的出现。

## 代码示例 (Python)

```python
def KMPSearch(pat, txt):
    M = len(pat)
    N = len(txt)
    lps = [0] * M
    j = 0  # index for pat[]
    computeLPSArray(pat, M, lps)
    i = 0  # index for txt[]
    while i < N:
        if pat[j] == txt[i]:
            i += 1
            j += 1
        if j == M:
            print("在索引 " + str(i - j) + " 处找到模式")
            j = lps[j - 1]
        elif i < N and pat[j] != txt[i]:
            if j != 0:
                j = lps[j - 1]
            else:
                i += 1

def computeLPSArray(pat, M, lps):
    length = 0  # length of the previous longest prefix suffix
    lps[0] = 0  # lps[0] 始终为 0
    i = 1
    while i < M:
        if pat[i] == pat[length]:
            length += 1
            lps[i] = length
            i += 1
        else:
            if length != 0:
                length = lps[length - 1]
            else:
                lps[i] = 0
                i += 1
```

## 代码示例 (Java)

```java
class KMP {
    void KMPSearch(String pat, String txt) {
        int M = pat.length();
        int N = txt.length();
        int lps[] = new int[M];
        int j = 0;
        computeLPSArray(pat, M, lps);
        int i = 0;
        while (i < N) {
            if (pat.charAt(j) == txt.charAt(i)) {
                i++;
                j++;
            }
            if (j == M) {
                System.out.println("在索引 " + (i - j) + " 处找到模式");
                j = lps[j - 1];
            } else if (i < N && pat.charAt(j) != txt.charAt(i)) {
                if (j != 0)
                    j = lps[j - 1];
                else
                    i = i + 1;
            }
        }
    }

    void computeLPSArray(String pat, int M, int lps[]) {
        int len = 0;
        int i = 1;
        lps[0] = 0;
        while (i < M) {
            if (pat.charAt(i) == pat.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len != 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }

    public static void main(String args[]) {
        String txt = "ABABDABACDABABCABAB";
        String pat = "ABABCABAB";
        new KMP().KMPSearch(pat, txt);
    }
}
```

## 代码示例 (C)

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

void computeLPSArray(char *pat, int M, int *lps) {
    int len = 0;
    int i = 1;
    lps[0] = 0;
    while (i < M) {
        if (pat[i] == pat[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                len = lps[len - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
}

void KMPSearch(char *pat, char *txt) {
    int M = strlen(pat);
    int N = strlen(txt);
    int *lps = (int *)malloc(sizeof(int) * M);
    int j = 0;
    computeLPSArray(pat, M, lps);
    int i = 0;
    while (i < N) {
        if (pat[j] == txt[i]) {
            i++;
            j++;
        }
        if (j == M) {
            printf("在索引 %d 处找到模式 \n", i - j);
            j = lps[j - 1];
        } else if (i < N && pat[j] != txt[i]) {
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }
    free(lps);
}

int main() {
    char txt[] = "ABABDABACDABABCABAB";
    char pat[] = "ABABCABAB";
    KMPSearch(pat, txt);
    return 0;
}
```

## 代码示例 (C++)

```cpp
#include <iostream>
#include <string>
#include <vector>

void computeLPSArray(std::string pat, int M, std::vector<int>& lps) {
    int len = 0;
    int i = 1;
    lps[0] = 0;
    while (i < M) {
        if (pat[i] == pat[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                len = lps[len - 1];
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
}

void KMPSearch(std::string pat, std::string txt) {
    int M = pat.length();
    int N = txt.length();
    std::vector<int> lps(M);
    computeLPSArray(pat, M, lps);
    int i = 0;
    int j = 0;
    while (i < N) {
        if (pat[j] == txt[i]) {
            i++;
            j++;
        }
        if (j == M) {
            std::cout << "在索引 " << i - j << " 处找到模式" << std::endl;
            j = lps[j - 1];
        } else if (i < N && pat[j] != txt[i]) {
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }
}

int main() {
    std::string txt = "ABABDABACDABABCABAB";
    std::string pat = "ABABCABAB";
    KMPSearch(pat, txt);
    return 0;
}
```

## 时间复杂度

KMP 算法的时间复杂度为 O(N + M)，其中 N 是文本字符串的长度，M 是模式的长度。

## 空间复杂度

KMP 算法的空间复杂度为 O(M)，其中 M 是模式的长度。 这是由于 LPS（最长公共前缀也是后缀）数组所需的空间。

## 使用场景

1.  在文本中搜索子字符串。
2.  在 DNA 序列中查找模式。
3.  抄袭检测。
4.  网络安全中的模式匹配。
