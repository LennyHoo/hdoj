# 1061 Rightmost Digit

### **Problem Description**

```
Given a positive integer N, you should output the most right digit of N^N.
```

### **Input**

```
The input contains several test cases. The first line of the input is a single integer T which is the number of test cases. T test cases follow.
Each test case contains a single positive integer N(1<=N<=1,000,000,000).
```

### **Output**

```
For each test case, you should output the rightmost digit of N^N.
```

### **Sample Input**

```
2
3
4
```

### **Sample Output**

```
7
6
```

### Notes

```
打表
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;

vector<int> res[10] = {{0},
                       {1},
                       {2, 4, 8, 6},
                       {3, 9, 7, 1},
                       {4, 6},
                       {5},
                       {6},
                       {7, 9, 3, 1},
                       {8, 4, 2, 6},
                       {9, 1}};

int main(){
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        size_t pos = n%(res[n%10].size());
        pos = (pos)?(pos-1):(res[n%10].size()-1);
        cout << res[n%10][pos] << endl;
    }
    return 0;
}
```

