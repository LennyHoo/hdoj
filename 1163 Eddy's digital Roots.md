# 1163 Eddy's digital Roots

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1163
```

### Notes

```
一个数对九取余后的结果称为九余数。
一个数的各位数字之和相加后得到的<10的数字称为这个数的九余数（如果相加结果大于9，则继续各位相加）
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;



int main()
{
    while(true){
        int n;
        cin >> n;
        if(!n)  return 0;
        int res = 1;
        for(int i=0; i<n; ++i){
            res = (res%9*n%9)%9;
        }
        if(!res) res = 9;
        printf("%d\n", res);
    }
    return 0;
}
```

