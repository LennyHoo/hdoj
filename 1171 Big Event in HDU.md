# 1171 Big Event in HDU

### **Problem Description**

```
Nowadays, we all know that Computer College is the biggest department in HDU. But, 
maybe you don't know that Computer College had ever been split into Computer College 
and Software College in 2002.
The splitting is absolutely a big event in HDU! At the same time, it is a trouble 
thing too. All facilities must go halves. First, all facilities are assessed, and two 
facilities are thought to be same if they have the same value. It is assumed that 
there is N (0<N<1000) kinds of facilities (different value, different kinds).
```

### **Input**

```
Input contains multiple test cases. Each test case starts with a number N (0 < N <= 50 
-- the total number of different facilities). The next N lines contain an integer V 
(0<V<=50 --value of facility) and an integer M (0<M<=100 --corresponding number of the 
facilities) each. You can assume that all V are different.
A test case starting with a negative integer terminates input and this test case is 
not to be processed.
```

### **Output**

```
For each case, print one line containing two integers A and B which denote the value 
of Computer College and Software College will get respectively. A and B should be as 
equal as possible. At the same time, you should guarantee that A is not less than B.
```

### **Sample Input**

```
2
10 1
20 1
3
10 1 
20 2
30 1
-1
```

### **Sample Output**

```
20 10
40 40
```

### Notes

```
母函数
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;


int main(){
    while(true){
        int n;
        cin >> n;
        if(n<0) return 0;
        vector<int> num(n);
        vector<int> value(n);
        int total = 0;
        for(int i=0; i<n; ++i){
            cin >> value[i] >> num[i];
            total += value[i]*num[i];
        }
        vector<int> a(total+1, 0);
        vector<int> b(total+1, 0);
        a[0] = 1;
        for(int i=0; i<n; ++i){
            for(int j=0; j<=num[i]&&j*value[i]<=total; ++j){
                for(int k=0; k+j*value[i]<=total; ++k){
                    b[k+j*value[i]] += a[k];
                }
            }
            a = b;
            b = vector<int>(total+1, 0);
        }
        int pos = ceil(total/2.f);
        while(!a[pos])  ++pos;
        cout << pos << " " << total-pos << endl;
    }
    return 0;
}
```

