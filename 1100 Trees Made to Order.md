# 1100 Trees Made to Order

### **Problem Description**

```
We can number binary trees using the following scheme:
The empty tree is numbered 0.
The single-node tree is numbered 1.
All binary trees having m nodes have numbers less than all those having m+1 nodes.
Any binary tree having m nodes with left and right subtrees L and R is numbered n such that all trees having m nodes numbered > n have either
Left subtrees numbered higher than L, or
A left subtree = L and a right subtree numbered higher than R.

The first 10 binary trees and tree number 20 in this sequence are shown below:

							img
							
Your job for this problem is to output a binary tree when given its order number.
```

### **Input**

```
Input consists of multiple problem instances. Each instance consists of a single integer n, where 1 <= n <= 500,000,000. A value of n = 0 terminates input. (Note that this means you will never have to output the empty tree.)
```

### **Output**

```
For each problem instance, you should output one line containing the tree corresponding to the order number for that instance. To print out the tree, use the following scheme:

A tree with no children should be output as X.
A tree with left and right subtrees L and R should be output as (L')X(R'), where L' and R' are the representations of L and R.
If L is empty, just output X(R').
If R is empty, just output (L')X.
```

### **Sample Input**

```
1
20
31117532
0
```

### **Sample Output**

```
X
((X)X(X))X
(X(X(((X(X))X(X))X(X))))X(((X((X)X((X)X)))X)X)
```

### Notes

```
dfs + dp
找到当前编号所对应的左孩子和右孩子，依次递归下去。
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;

vector<int64_t> types;
vector<int64_t> numberStart;

void init(int64_t m){
    types = vector<int64_t>(m+1, 0);
    numberStart = vector<int64_t>(m+1);
    types[0] = 1;
    types[1] = 1;
    numberStart[0] = 0;
    numberStart[1] = 1;
    for(int64_t i=2; i<=m; ++i){
        for(int64_t j=0; j<=i-1; ++j){
            types[i] += types[j]*types[i-1-j];
        }
        numberStart[i] = numberStart[i-1] + types[i-1];
    }
}


pair<int64_t, int64_t> match(int64_t n){
    int64_t m = 0;
    while(numberStart[m+1]<=n)
        ++m;
    int64_t start = numberStart[m]-1;
    for(int64_t i=0; i<m; ++i){
        if(start+types[i]*types[m-1-i]<n){
            start += types[i]*types[m-1-i];
            continue;
        }
        for(int64_t left=numberStart[i]; left<numberStart[i+1]; ++left){
            for(int64_t right=numberStart[m-1-i]; right<numberStart[m-i]; ++right){
                if(++start==n)
                    return make_pair(left, right);
            }
        }
    }
    return make_pair(-1, -1);
}

string dfs(int64_t n){
    string res = "X";
    if(n==1)    return res;
    pair<int64_t, int64_t> children = match(n);
    if(children.first>0)
        res = "(" + dfs(children.first) + ")" + res;
    if(children.second>0)
        res = res + "(" + dfs(children.second) + ")";
    return res;
}

int main(){
    init(105);
    while(true){
        int64_t n;
        cin >> n;
        if(!n) return 0;
        cout << dfs(n) << endl;
    }
    return 0;
}
```

