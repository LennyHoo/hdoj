# 1030 Delta-wave

### **Problem Description**

```
A triangle field is numbered with successive integers in the way shown on the picture below.

The traveller needs to go from the cell with number M to the cell with number N. The traveller is able to enter the cell through cell edges only, he can not travel from cell to cell through vertices. The number of edges the traveller passes makes the length of the traveller's route.

Write the program to determine the length of the shortest route connecting cells with numbers N and M.
```

### **Input**

```
Input contains two integer numbers M and N in the range from 1 to 1000000000 separated with space(s).
```

### **Output**

```
Output should contain the length of the shortest route.
```

### **Sample Input**

```
6 12
```

### **Sample Output**

```
3
```

### Notes

```
① 第 n 行最后一个数字是 n^2
② 所以，第 n 行第一个数字是 (n-1)^2+1

对于一个数字 x， 它位于第 n 行，那么有：
   ③ 行数 n = sqrt(x-1) + 1
   ④ 因为从左边开始，每经过两个数字，左坐标增加1，所以 x 的左坐标是：
         (x-((n-1)^2+1))/2
   ⑤ 因为从右边开始，每经过两个数字，右坐标增加1，所以 x 的右坐标是：
         (n^2-x)/2
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;


int main(){
    int64_t n, m;
    while(cin>>n>>m){
        int64_t levelN = sqrt(n-1)+1;
        int64_t levelM = sqrt(m-1)+1;
        int64_t leftN = (n-(pow(levelN-1, 2)+1))/2;
        int64_t leftM = (m-(pow(levelM-1, 2)+1))/2;
        int64_t rightN = (pow(levelN, 2)-n)/2;
        int64_t rightM = (pow(levelM, 2)-m)/2;
        int64_t res = abs(levelM-levelN)+abs(leftM-leftN)+abs(rightM-rightN);
        cout << res << endl;
    }
    return 0;
}
```

