# 1098 Ignatius's puzzle

### **Problem Description**

```
Ignatius is poor at math,he falls across a puzzle problem,so he has no choice but to appeal to Eddy. this problem describes that:f(x)=5*x^13+13*x^5+k*a*x,input a nonegative integer k(k<10000),to find the minimal nonegative integer a,make the arbitrary integer x ,65|f(x)if
no exists that a,then print "no".
```

### **Input**

```
The input contains several test cases. Each test case consists of a nonegative integer k, More details in the Sample Input.
```

### **Output**

```
The output contains a string "no",if you can't find a,or you should output a line contains the a.More details in the Sample Output.
```

### **Sample Input**

```
11
100
9999
```

### **Sample Output**

```
22
no
43
```

### Notes

```
因为 65|f(x) 对于任意x成立，因此枚举a从1到65，试探是否在x=1处成立。 
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;


int main(){
    int k;
    while(cin>>k){
        bool no = true;
        for(int a=1; a<=65; ++a){
            if((18+a*k)%65==0){
                cout << a << endl;
                no = false;
                break;
            }
        }
        if(no)
            cout << "no" << endl;
    }
    return 0;
}
```

