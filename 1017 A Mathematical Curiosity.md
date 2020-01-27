# 1017 A Mathematical Curiosity

### **Problem Description**

```
Given two integers n and m, count the number of pairs of integers (a,b) such that 0 < a < b < n and (a^2+b^2 +m)/(ab) is an integer.

This problem contains multiple test cases!

The first line of a multiple input is an integer N, then a blank line followed by N input blocks. Each input block is in the format indicated in the problem description. There is a blank line between input blocks.

The output format consists of N output blocks. There is a blank line between output blocks.
```

### **Input**

```
You will be given a number of cases in the input. Each case is specified by a line containing the integers n and m. The end of input is indicated by a case in which n = m = 0. You may assume that 0 < n <= 100.
```

### **Output**

```
For each case, print the case number as well as the number of pairs (a,b) satisfying the given property. Print the output for each case on one line in the format as shown below.
```

### **Sample Input**

```
1

10 1
20 3
30 4
0 0
```

### **Sample Output**

```
Case 1: 2
Case 2: 4
Case 3: 5
```

### Notes

```
水题，但是格式没有说明清楚，很坑。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;


int main(){
    int n{};
    cin >> n;
    for(int i=0; i<n; ++i){
        int kCase = 1;
        while(true){
            int n, m;
            cin >> n >> m;
            int cnt = 0;
            if(!n&&!m)  break;
            for(int a=1; a<n-1; ++a){
                for(int b=a+1; b<n; ++b){
                    if(!((a*a+b*b+m)%(a*b)))
                        ++cnt;
                }
            }
            printf("Case %d: %d\n", kCase++, cnt);
        }
        if(i!=n-1)  printf("\n");
    }
    return 0;
}
```

