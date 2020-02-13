# 1152 Brownie Points I

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1152
```

### Notes

```
理解题意就行，水题。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

struct Node{
    int x;
    int y;
};

bool cmp_x(const Node &a, const Node &b){
    return (a.x<b.x);
}

bool cmp_y(const Node &a, const Node &b){
    return (a.y<b.y);
}

int main()
{
    while(true){
        int n;
        cin >> n;
        if(!n)  return 0;
        vector<Node> nodes(n);
        for(int i=0; i<n; ++i)
            cin >> nodes[i].x >> nodes[i].y;
        int middle_x = nodes[n/2].x;
        int middle_y = nodes[n/2].y;
        int stan = 0, ollie = 0;
        for(int i=0; i<n; ++i){
            if(nodes[i].x>middle_x&&nodes[i].y>middle_y)
                ++stan;
            else if(nodes[i].x<middle_x&&nodes[i].y<middle_y)
                ++stan;c++
            else{
                if(nodes[i].x!=middle_x&&nodes[i].y!=middle_y)
                    ++ollie;
            }
        }
        printf("%d %d\n", stan, ollie);
    }
    return 0;
}
```

