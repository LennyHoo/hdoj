# 1005 Number Sequence

### **Problem Description**
```
A number sequence is defined as follows:

f(1) = 1, f(2) = 1, f(n) = (A * f(n - 1) + B * f(n - 2)) mod 7.

Given A, B, and n, you are to calculate the value of f(n).
```
### **Input**
```
The input consists of multiple test cases. Each test case contains 3 integers A, B and n on a single line (1 <= A, B <= 1000, 1 <= n <= 100,000,000). Three zeros signal the end of input and this test case is not to be processed.
```
### **Output**
```
For each test case, print the value of f(n) on a single line.
```
### **Sample Input**

```
1 1 3
1 2 10
0 0 0
```

### **Sample Output**

```
2
5
```

### Notes
```
看了 Discuss，有人说 余到万时结果一样 ，竟然真的可行。
```
### Code

```c++
#include <iostream>
#include "cstdio"

using namespace std;

int helper(int a, int b, int n){
    if(n==1||n==2)  return 1;
    while(n>10000)  n/=10;
    int p = 1;
    int q = 1;
    for(int i=3; i<=n; ++i){
        int temp = q;
        q = (a*q + b*p)%7;
        p = temp;
    }
    return q;
}

int main() {
    int a{};
    int b{};
    int n{};
    while(true){
        cin >> a >> b >> n;
        if(!a&&!b&&!n)  return 0;
        cout << helper(a, b, n) << endl;
    }
}
```

