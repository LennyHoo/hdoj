# 1060 Leftmost Digit

### **Problem Description**

```
Given a positive integer N, you should output the leftmost digit of N^N.
```

### **Input**

```
The input contains several test cases. The first line of the input is a single integer T which is the number of test cases. T test cases follow.
Each test case contains a single positive integer N(1<=N<=1,000,000,000).
```

### **Output**

```
For each test case, you should output the leftmost digit of N^N.
```

### **Sample Input**

```
2
3
4
```

### Sample Output

```
2
2
```

### Notes

```
N^(N)对10取对数可以表示成 N*lg(N) = m + lg(a);
所以N^(N)又可以是10^(m+lg(a)) = a*10^(m),也就是科学计数法。
所以a的最左侧的数就是N^(N)的最左侧的数。
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
        double n;
        cin >> n;
        double log10_pow_n_n = n*log10(n);
        auto integer = (long long)log10_pow_n_n;
        double rest = log10_pow_n_n - integer;
        int res = (int)pow(10, rest);
        cout << res << endl;
    }
}
```

