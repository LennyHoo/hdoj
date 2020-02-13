# 1128 Self Numbers

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1128
```

### Notes

```
由一个数生成的数字肯定比这个数大，所以可以遍历 1 到 1000000，一边标记所生成的数(非self number)，一边判断当前的数是否是self number。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

const int N = 1000000;
vector<bool> vis(N, false);

int64_t generate(int n){
    int res = n;
    while(n){
        res += n%10;
        n /= 10;
    }
    return res;
}


int main()
{
    for(int64_t i=1; i<=N; ++i){
        int num = generate(i);
        if(num<N)
            vis[num] = true;
        if(!vis[i])
            printf("%lldn", i);
    }
    return 0;
}
```

