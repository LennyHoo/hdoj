# 1179 Ollivanders: Makers of Fine Wands since 382 BC.

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1179
```

### Notes

```
匈牙利算法
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

const int MAX = 105;
bool edge[MAX][MAX];
int link[MAX];
bool vis[MAX];
int n, m;

bool dfs(int x){
    for(int i=0; i<n; ++i){
        if(!vis[i]&&edge[x][i]){
            vis[i] = true;
            if(link[i]==-1||dfs(link[i])){
                link[i] = x;
                return true;
            }
        }
    }
    return false;
}

int hungary(){
    int res = 0;
    memset(link, -1, sizeof(link));
    for(int i=0; i<m; ++i){
        memset(vis, false, sizeof(vis));
        if(dfs(i))  ++res;
    }
    return res;
}

int main()
{
    while(cin>>n>>m){
        memset(edge, false, sizeof(edge));
        for(int i=0; i<m; ++i){
            int k;
            cin >> k;
            while(k--){
                int j;
                cin >> j;
                edge[i][j-1] = true;
            }
        }
        printf("%d\n", hungary());
    }
    return 0;
}
```

