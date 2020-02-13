# 1141 Factstone Benchmark

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1141
```

### Notes

```
用对数化简公式：
	lg(n!) = lg(1) + lg(2) + ... + lg(n-1) + lg(n);
	lg(2^n-1)约等于 lg(2^n) = n*lg(2);
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


int main()
{
    while(true){
        int year;
        cin >> year;
        if(!year) return 0;
        int n = (year-1960)/10+2;
        double log10MaxNum = pow(2, n)*log10(2);
        int res;
        double sum = 0.f;
        for(res=1; sum+2*log10(res)<log10MaxNum; ++res)
            sum += log10(res);
        printf("%d\n", res);
    }
    return 0;
}
```

