# 1114 Piggy-Bank

### Problem Description

```
http://acm.hdu.edu.cn/showproblem.php?pid=1114
```

### Notes

```
完全背包，求最小值问题。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

struct Coin{
    int weight;
    int value;
};

int main()
{
    int t;
    cin >> t;
    while(t--){
        int emptyWeight, fullWeight;
        cin >> emptyWeight >> fullWeight;
        int volume = (fullWeight-emptyWeight);
        int n;
        cin >> n;
        vector<Coin> coins(n+1);
        for(int i=1; i<=n; ++i)
            cin >> coins[i].value >> coins[i].weight;
        vector<int64_t> dp(volume+1, INT_MAX);
        dp[0] = 0;
        for(int i=1; i<=n; ++i){
            int weight = coins[i].weight;
            int value = coins[i].value;
            for(int j=weight; j<=volume; ++j){
                dp[j] = min(dp[j], dp[j-weight]+value);
            }
        }
        if(dp[volume]>=INT_MAX)    
            printf("This is impossible.\n");
        else 
            printf("The minimum amount of money in the piggy-bank is %d.\n", dp[volume]);
    }
    return 0;
}
```

