# 1110 Equipment Box

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1110
```

### Notes

```
特殊情况直接判断，其余的暴力枚举。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

#define PI 3.1415926

bool judge(double a, double b, double c, double d){
    if(a*b<=c*d) return false;
    if(a>b) swap(a, b);
    if(c>d) swap(c, d); 
    if(a>c&&b>d)
        return true;
    for(double angle=0.f; angle<=90.f; angle+=0.2){
        double rad = PI*angle/180.f;
        double w = c*sin(rad)+d*cos(rad);
        double h = c*cos(rad)+d*sin(rad);
        if(w<a&&h<b)  return true;
    }
    return false;
}

int main()
{
    int n;
    cin >> n;
    while(n--){
        double a, b, c, d;
        bool res;
        cin >> a >> b >> c >> d;
        if(judge(a, b, c, d))
            printf("Escape is possible.\n");
        else 
            printf("Box cannot be dropped.\n");
    }
    return 0;
}
```

