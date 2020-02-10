# 1054 Strategic Game

### **Problem Description**

```
Bob enjoys playing computer games, especially strategic games, but sometimes he cannot find the solution fast enough and then he is very sad. Now he has the following problem. He must defend a medieval city, the roads of which form a tree. He has to put the minimum number of soldiers on the nodes so that they can observe all the edges. Can you help him?

Your program should find the minimum number of soldiers that Bob has to put for a given tree.

The input file contains several data sets in text format. Each data set represents a tree with the following description:

the number of nodes
the description of each node in the following format
node_identifier:(number_of_roads) node_identifier1 node_identifier2 ... node_identifier
or
node_identifier:(0)

The node identifiers are integer numbers between 0 and n-1, for n nodes (0 < n <= 1500). Every edge appears only once in the input data.

For example for the tree:
 
           0

           1

      2          3
    
the solution is one soldier ( at the node 1).

The output should be printed on the standard output. For each given input data set, print one integer number in a single line that gives the result (the minimum number of soldiers). An example is given in the following table:
```

### **Sample Input**

```
4
0:(1) 1
1:(2) 2 3
2:(0)
3:(0)
5
3:(3) 1 4 2
1:(1) 0
2:(0)
0:(0)
4:(0)
```

### **Sample Output**

```
1
2
```

### Notes

```
树形dp，初始化：
	dp[father][0] = 0;   // 0 代表不在这个结点放置士兵
    dp[father][1] = 1;    // 1 代表在这个结点放置士兵
状态转移方程：
	dp[father][0] += dp[child][1];    // 显然父节点不放，则子节点全部都要放
    dp[father][1] += min(dp[child][0], dp[child][1]);  // 父节点放了，子节点可放可不放
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;

vector<int> children[1505];
bool hasFather[1505] = {false};
int dp[1505][2];

void dfs(int root){
    dp[root][0] = 0;   // 0 代表不在这个结点放置士兵
    dp[root][1] = 1;    // 1 代表在这个结点放置士兵
    if(children[root].empty()) return;
    for(int child : children[root]){
        dfs(child);
        dp[root][0] += dp[child][1];    // 显然父节点不放，则子节点全部都要放
        dp[root][1] += min(dp[child][0], dp[child][1]);  // 父节点放了，子节点可放可不放
    }
}

int main(){
    int n;
    while(cin>>n){
        memset(hasFather, false, sizeof(hasFather));
        memset(dp, 0, sizeof(dp));
        while(n--){
            int father;
            cin >> father;
            getchar();
            getchar();
            int sonNum;
            cin >> sonNum;
            getchar();
            children[father].clear();
            while(sonNum--){
                int child;
                cin >> child;
                children[father].emplace_back(child);
                hasFather[child] = true;
            }
        }
        // 找到根节点
        int root = 0;
        while(hasFather[root])  ++root;
        dfs(root);
        cout << min(dp[root][0], dp[root][1]) << endl;
    }
    return 0;
}
```

