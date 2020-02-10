# 1081 To The Max

### **Problem Description**

```
Given a two-dimensional array of positive and negative integers, a sub-rectangle is any contiguous sub-array of size 1 x 1 or greater located within the whole array. The sum of a rectangle is the sum of all the elements in that rectangle. In this problem the sub-rectangle with the largest sum is referred to as the maximal sub-rectangle.

As an example, the maximal sub-rectangle of the array:

0 -2 -7 0
9 2 -6 2
-4 1 -4 1
-1 8 0 -2

is in the lower left corner:

9 2
-4 1
-1 8

and has a sum of 15.
```

### **Input**

```
The input consists of an N x N array of integers. The input begins with a single positive integer N on a line by itself, indicating the size of the square two-dimensional array. This is followed by N 2 integers separated by whitespace (spaces and newlines). These are the N 2 integers of the array, presented in row-major order. That is, all numbers in the first row, left to right, then all numbers in the second row, left to right, etc. N may be as large as 100. The numbers in the array will be in the range [-127,127].
```

### **Output**

```
Output the sum of the maximal sub-rectangle.
```

### **Sample Input**

```
4
0 -2 -7 0 9 2 -6 2
-4 1 -4 1 -1
8 0 -2
```

### **Sample Output**

```
15
```

### Notes

```
① 每列以前缀和的形式储存在二维矩阵中。
② 将二维矩阵压缩成一维的形式（前缀和作差）。
③ 动态规划求子矩阵和的最大值。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

int main() {
    int n;
    while(cin >> n){
        vector<vector<int>> nums(n+1, vector<int>(n));
        for(int i=0; i<n; ++i)
            nums[0][i] = 0;
        // 分别计算每列的前缀和储存在二维数组中
        for(int i=1; i<=n; ++i){
            for(int j=0; j<n; ++j){
                int num;
                cin >> num;
                nums[i][j] = nums[i-1][j] + num;
            }
        }
        int maxSum = INT_MIN;
        // 降维
        vector<int> array = vector<int>(n, 0);
        for(int i=0; i<n; ++i){
            for(int j=i+1; j<=n; ++j){
                for(int k=0; k<n; ++k){
                    array[k] = nums[j][k] - nums[i][k];
                }
                // 动态规划
                int sum = 0;
                for(int u=0; u<n; ++u){
                    sum += array[u];
                    maxSum = max(maxSum, sum);
                    if(sum<0)
                        sum = 0;
                }
            }
        }
        cout << maxSum << endl;
    }
    return 0;
}
```

