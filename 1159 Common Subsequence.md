# 1159 Common Subsequence

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1159
```

### Notes

```
LCS
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;



int main()
{
    string a, b;
    while(cin>>a>>b){
        int m = a.size();
        int n = b.size();
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        for(int i=1; i<=m; ++i){
            for(int j=1; j<=n; ++j){
                if(a[i-1]==b[j-1])
                    dp[i][j] = dp[i-1][j-1] + 1;
                else{
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
                }
            }
        }
        printf("%d\n", dp[m][n]);
    }
    return 0;
}
```

