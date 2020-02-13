# 1158 Employment Planning

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1158
```

### Notes

```
dp
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
        int hire, salary, fire;
        scanf("%d %d %d", &hire, &salary, &fire);
        int minNum = INT_MAX;
        int maxNum = INT_MIN;
        vector<int> need(n+1);
        for(int i=1; i<=n; ++i){
            scanf("%d", &need[i]);
            minNum = min(minNum, need[i]);
            maxNum = max(maxNum, need[i]);
        }
        vector<vector<int>> dp(n+1, vector<int>(maxNum+1, INT_MAX));
        for(int j=minNum; j<=maxNum; ++j)
            dp[1][j] = (hire+salary)*j;
        for(int i=2; i<=n; ++i){
            for(int j=need[i]; j<=maxNum; ++j){
                for(int k=need[i-1]; k<=maxNum; ++k){
                    int value = (k>j)?(fire):(hire);
                    dp[i][j] = min(dp[i][j], dp[i-1][k]+abs(k-j)*value+j*salary);
                }
            }
        }
        int res = INT_MAX;
        for(int i=need[n]; i<=maxNum; ++i){
            res = min(res, dp[n][i]);
        }
        printf("%d\n", res);
    }
    return 0;
}
```

