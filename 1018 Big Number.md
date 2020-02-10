# 1018 Big Number

### **Problem Description**

```
In many applications very large integers numbers are required. Some of these applications are using keys for secure transmission of data, encryption, etc.In this problem you are given a number, you have to determine the number of digits in the factorial of the number.
```

### **Input**

```
Input consists of several lines of integer numbers. The first line contains an integer n, which is the number of cases to be tested, followed by n lines, one integer 1 ≤ n ≤ 107 on each line.
```

### **Output**

```
The output contains the number of digits in the factorial of the integers appearing in the input.
```

### **Sample Input**

```
2
10
20
```

### **Sample Output**

```
7
19
```

### Notes

```
n! = n*(n-1)*(n-2)*...*2*1
lg(n!) = lg(n) + lg(n-1) + ... + lg(2) + lg(1) = m + lg(a)	(整数和小数两部分)
n! = 10^(m+lg(a)) = a*10^(m)
所以 n! 有 m+1 位数字。
```

### Code

```c++
#include <iostream>
#include "cstdio"
#include "cmath"

using namespace std;


int main() {
    int t{};
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        double sum = 0;
        for(int i=2; i<=n; ++i)
            sum += log10(i);
        auto number = (long long)sum + 1;
        cout << number << endl;
    }
}
```

