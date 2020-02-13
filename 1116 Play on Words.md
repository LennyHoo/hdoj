# 1116 Play on Words

### Problem Description

```
http://acm.hdu.edu.cn/showproblem.php?pid=1116
```

### Notes

```
并查集 +　欧拉回路(通路)的判定。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

class DisjointSet{
private:
    vector<int> parent;
    vector<bool> vis;
public:
    DisjointSet(int n){
        parent = vector<int>(n, -1);
        vis = vector<bool>(n, false);
    }
    int findRoot(int x){
        vis[x] = true;
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
        for(int i=0; i<parent.size(); ++i){
            if(parent[i]==-1&&vis[i])
                ++res;
        }
        return res;
    }
};

struct Degree{
    int in;
    int out;
    explicit Degree(int in=0, int out=0){
        this->in = in;
        this->out = out;
    }
};

int main()
{
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        DisjointSet disjointSet(26);
        map<char, Degree> table;
        for(int i=0; i<n; ++i){
            string s;
            cin >> s;
            char from = *s.begin();
            char to = *(s.end()-1);
            disjointSet.merge(from-'a', to-'a');
            auto it = table.find(from);
            if(it==table.end())
                table.insert(make_pair(from, Degree(0, 1)));
            else
                ++it->second.out;
            it = table.find(to);
            if(it==table.end())
                table.insert(make_pair(to, Degree(1, 0)));
            else 
                ++it->second.in;
        }
        int groupNum = disjointSet.groupNum();
        if(groupNum>1){
            printf("The door cannot be opened.\n");
            continue;
        }
        bool res = true;
        int start = -1, end = -1;
        for(auto it=table.begin(); it!=table.end(); ++it){
            if(abs(it->second.in-it->second.out)>1){
                res = false;
                break;
            }
            else{
                if(it->second.in-it->second.out==1){
                    if(end==-1) end = distance(table.begin(), it);
                    else{
                        res = false;
                        break;
                    }
                }
                if(it->second.in-it->second.out==-1){
                    if(start==-1)   start = distance(table.begin(), it);
                    else{
                        res = false;
                        break;
                    }
                }
            }
        }
        if(res)
            printf("Ordering is possible.\n");
        else 
            printf("The door cannot be opened.\n");
    }
    return 0;
}
```

