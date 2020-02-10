# 1078 FatMouse and Cheese

### **Problem Description**

```
FatMouse has stored some cheese in a city. The city can be considered as a square grid of dimension n: each grid location is labelled (p,q) where 0 <= p < n and 0 <= q < n. At each grid location Fatmouse has hid between 0 and 100 blocks of cheese in a hole. Now he's going to enjoy his favorite food.

FatMouse begins by standing at location (0,0). He eats up the cheese where he stands and then runs either horizontally or vertically to another location. The problem is that there is a super Cat named Top Killer sitting near his hole, so each time he can run at most k locations to get into the hole before being caught by Top Killer. What is worse -- after eating up the cheese at one location, FatMouse gets fatter. So in order to gain enough energy for his next run, he has to run to a location which have more blocks of cheese than those that were at the current hole.

Given n, k, and the number of blocks of cheese at each grid location, compute the maximum amount of cheese FatMouse can eat before being unable to move.
```

### **Input**

```
There are several test cases. Each test case consists of

a line containing two integers between 1 and 100: n and k
n lines, each with n numbers: the first line contains the number of blocks of cheese at locations (0,0) (0,1) ... (0,n-1); the next line contains the number of blocks of cheese at locations (1,0), (1,1), ... (1,n-1), and so on.
The input ends with a pair of -1's.
```

### **Output**

```
For each test case output in a line the single integer giving the number of blocks of cheese collected.
```

### **Sample Input**

```
3 1
1 2 5
10 11 6
12 12 7
-1 -1
```

### **Sample Output**

```
37
```

### Notes

```
记忆化搜索
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;

int n, k;
int grid[110][110];
int dp[110][110];
int dx[] = {1, -1, 0, 0};
int dy[] = {0, 0, 1, -1};

bool legal(int i, int j){
    return (i>=0&&i<n&&j>=0&&j<n);
}

int dfs(int i, int j){
    if(dp[i][j]!=-1)
        return dp[i][j];
    dp[i][j] = grid[i][j];
    for(int u=1; u<=k; ++u){
        for(int v=0; v<4; ++v){
            int newI = i + dx[v]*u;
            int newJ = j + dy[v]*u;
            if(legal(newI, newJ)&&grid[newI][newJ]>grid[i][j])
                dp[i][j] = max(dp[i][j], grid[i][j]+dfs(newI, newJ));
        }
    }
    return dp[i][j];
}

int main(){
    while(true){
        cin >> n >> k;
        if(n==-1&&k==-1)
            return 0;
        for(int i=0; i<n; ++i){
            for(int j=0; j<n; ++j)
                cin >> grid[i][j];
        }
        memset(dp, -1, sizeof(dp));
        cout <<  dfs(0, 0) << endl;
    }
    return 0;
}
```

