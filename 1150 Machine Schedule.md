# 1150 Machine Schedule

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1150
```

### Notes

```
最小顶点覆盖 = 最大匹配数
```

#### Code

```c++
#include "bits/stdc++.h"

using namespace std;

const int N = 105;

bool edge[N][N];
int link[N];
bool vis[N];
int n, m, k;


bool dfs(int x){
    for(int i=0; i<m; ++i){
        if(edge[x][i]&&!vis[i]){
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
    for(int i=0; i<n; ++i){
        memset(vis, false, sizeof(vis));
        if(dfs(i))  ++res;
    }
    return res;
}

int main()
{
    while(true){
        cin >> n;
        if(!n)  return 0;
        cin >> m >> k;
        memset(edge, false, sizeof(edge));
        int hasZero = 0;
        while(k--){
            int i, x, y;
            cin >> i >> x >> y;
            edge[x][y] = true;
            if(!hasZero)
                hasZero = !x;
        }
        int res = hungary();
        printf("%d\n", res-hasZero);
    }
    return 0;
}
```

