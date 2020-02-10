# 1097 **Problem Description**

### **Problem Description**

```
lcy gives a hard puzzle to feng5166,lwg,JGShining and Ignatius: gave a and b,how to know the a^b.everybody objects to this BT problem,so lcy makes the problem easier than begin.
this puzzle describes that: gave a and b,how to know the a^b's the last digit number.But everybody is too lazy to slove this problem,so they remit to you who is wise.
```

### **Input**

```
There are mutiple test cases. Each test cases consists of two numbers a and b(0<a,b<=2^30)
```

### **Output**

```
For each test case, you should output the a^b's last digit number.
```

### **Sample Input**

```
7 66
8 800
```

### **Sample Output**

```
9
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
    int a, b;
    while(cin>>a>>b){
        size_t pos = b%(res[a%10].size());
        pos = (pos)?(pos-1):(res[a%10].size()-1);
        cout << res[a%10][pos] << endl;
    }
    return 0;
}
```

