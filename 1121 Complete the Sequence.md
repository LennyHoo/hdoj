# 1121 Complete the Sequence

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1121
```

### Notes

```
列表，先求差分到 n-1 次差分， 然后逆推回第一行。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


int main()
{
    int t;
    cin >> t;
    while(t--){
        int s, c;
        cin >> s >> c;
        vector<vector<int>> table(s, vector<int>(s+c));
        for(int i=0; i<s; ++i)
            cin >> table[0][i];
        for(int i=1; i<s; ++i){
            for(int j=0; j<s-i; ++j){
                table[i][j] = table[i-1][j+1]-table[i-1][j];
            }
        }
        for(int i=1; i<=c; ++i) 
            table[s-1][i] = table[s-1][0];
        for(int i=s-2; i>=0; --i){
            for(int j=s-i; j<s-i+c; ++j){
                table[i][j] = table[i][j-1]+table[i+1][j-1];
            }
        } 
        for(int i=0; i<c-1; ++i)
            printf("%d ", table[0][s+i]);
        printf("%d\n", table[0][s+c-1]);    
    }
    return 0;
}
```

