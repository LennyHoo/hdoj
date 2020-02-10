# 1016 Prime Ring Problem

### **Problem Description**

```
A ring is compose of n circles as shown in diagram. Put natural number 1, 2, ..., n into each circle separately, and the sum of numbers in two adjacent circles should be a prime.

Note: the number of first circle should always be 1.
```

### **Input**

```
n (0 < n < 20).
```

### **Output**

```
The output format is shown as sample below. Each row represents a series of circle numbers in the ring beginning from 1 clockwisely and anticlockwisely. The order of numbers must satisfy the above requirements. Print solutions in lexicographical order.

You are to write a program that completes above process.

Print a blank line after each case.
```

### **Sample Input**

```
6
8
```

### **Sample Output**

```
Case 1:
1 4 3 2 5 6
1 6 5 2 3 4

Case 2:
1 2 3 8 5 6 7 4
1 2 5 8 3 4 7 6
1 4 7 6 5 8 3 2
1 6 7 4 3 8 5 2
```

### Notes

```
本题主要思路是dfs，边界条件：step==n+1&&isPrime(res[1]+res[n])
特别应注意：第i个元素用完之后要回收，这样才能回溯。
```

### Code

```c++
#include <iostream>
#include "cstdio"
#include "cstring"

using namespace std;


bool isPrime(int n){
    for(int i=2; i<=n/2; ++i){
        if(n%i==0) return false;
    }
    return true;
}

int res[30];
int visited[30] = {0};
int n{};

void dfs(int step){
    // 边界条件
    if(step==n+1&&isPrime(res[1]+res[n])){
        for(int i=1; i<=n-1; ++i){
            printf("%d ", res[i]);
        }
        printf("%d\n", res[n]);
        return;
    }
    // 回溯
    for(int i=2; i<=n; ++i){
        // 剪枝
        if(!visited[i]){
            if(isPrime(i+res[step-1])){
                visited[i] = 1;
                res[step] = i;
                dfs(step+1);
                visited[i] = 0;  // 第i个元素用完之后回收
            }
        }
    }
}

int main() {
    int kCase = 0;
    res[1] = 1;
    while(cin>>n){
        printf("Case %d:\n", ++kCase);
        memset(visited, 0, sizeof(visited));
        dfs(2);
        printf("\n");
    }
    return 0;
}
```

