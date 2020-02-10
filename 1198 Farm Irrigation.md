# 1198 Farm Irrigation

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1198
```

### Notes

```
并查集
A negative M or N denotes the end of input，这里其实只要m或n是非正数就停止。
```

### Code

```c++
#include "iostream"
#include "vector"

using namespace std;

class DisjointSet{
private:
    vector<int> parent;
public:
    DisjointSet(int n){
        parent = vector<int>(n, -1);
    }
    int findRoot(int x){
        while(parent[x]!=-1)
            x = parent[x];
        return x;
    }
    bool merge(int x, int y){
        int x_root = findRoot(x);
        int y_root = findRoot(y);
        if(x_root==y_root)
            return false;
        else{
            parent[x_root] = y_root;
            return true;
        }
    }
    int groupNum(){
        int res = 0;
        for(int &c: parent){
            if(c==-1)   ++res;
        }
        return res;
    }
};

// 顺序是东南西北
int types[11][4] = {{0, 0, 1, 1},
                    {1, 0, 0, 1},
                    {0, 1, 1, 0},
                    {1, 1, 0, 0},
                    {0, 1, 0, 1},
                    {1, 0, 1, 0},
                    {1, 0, 1, 1},
                    {0, 1, 1, 1},
                    {1, 1, 1, 0},
                    {1, 1, 0, 1},
                    {1, 1, 1, 1}};

const int E = 0, S = 1, W = 2, N = 3;

int main()
{
    while(true){
        int n, m;
        cin >> n >> m;
        if(n<=0||m<=0)
            return 0;
        vector<vector<char>> grid(n, vector<char>(m));
        DisjointSet disjointSet(n*m);
        for(int i=0; i<n; ++i){
            for(int j=0; j<m; ++j){
                cin >> grid[i][j];
                int pos = i*m + j;
                int nowType = grid[i][j]-'A';
                if(j){
                    int leftPos = pos-1;
                    int leftType = grid[i][j-1]-'A';
                    if(types[leftType][E]&&types[nowType][W])
                        disjointSet.merge(pos, leftPos);
                }
                if(i){
                    int upPos = pos-m;
                    int upType = grid[i-1][j]-'A';
                    if(types[upType][S]&&types[nowType][N])
                        disjointSet.merge(pos, upPos);
                }
            }
        }
        int res = disjointSet.groupNum();
        printf("%d\n", res);
    }
    return 0;
}
```

