# 1213 How Many Tables

### **Problem Description**

```
Today is Ignatius' birthday. He invites a lot of friends. Now it's dinner time. 
Ignatius wants to know how many tables he needs at least. You have to notice that not 
all the friends know each other, and all the friends do not want to stay with 
strangers.

One important rule for this problem is that if I tell you A knows B, and B knows C, 
that means A, B, C know each other, so they can stay in one table.

For example: If I tell you A knows B, B knows C, and D knows E, so A, B, C can stay in 
one table, and D, E have to stay in the other one. So Ignatius needs 2 tables at 
least.
```

### **Input**

```
The input starts with an integer T(1<=T<=25) which indicate the number of test cases. 
Then T test cases follow. Each test case starts with two integers N and 
M(1<=N,M<=1000). N indicates the number of friends, the friends are marked from 1 to 
N. Then M lines follow. Each line consists of two integers A and B(A!=B), that means 
friend A and friend B know each other. There will be a blank line between two cases.
```

### **Output**

```
For each test case, just output how many tables Ignatius needs at least. Do NOT print 
any blanks.
```

### **Sample Input**

```
2
5 3
1 2
2 3
4 5

5 1
2 5
```

### **Sample Output**

```
2
4
```

### Notes

```
DisjointSet
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


class DisjointSet{
private:
    vector<int> parent;
public:
    DisjointSet(int n){
        parent = vector<int>(n+1, -1);
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
    int groupNums(){
        int res = 0;
        for(int i=1; i<parent.size(); ++i){
            if(parent[i]==-1)
                ++res;
        }
        return res;
    }
};

int main()
{
    int t;
    cin >> t;
    while(t--){
        int n, m;
        cin >> n >> m;
        DisjointSet disjointSet(n);
        while(m--){
            int a, b;
            cin >> a >> b;
            disjointSet.merge(a, b);
        }
        cout << disjointSet.groupNums() << endl;
    }
    return 0;
}
```

