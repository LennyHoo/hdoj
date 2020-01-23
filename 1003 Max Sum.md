# 1003 Max Sum

### **Problem Description**
```
Given a sequence a[1],a[2],a[3]......a[n], your job is to calculate the max sum of a sub-sequence. For example, given (6,-1,5,4,-7), the max sum in this sequence is 6 + (-1) + 5 + 4 = 14.
```
### **Input**
```
The first line of the input contains an integer T(1<=T<=20) which means the number of test cases. Then T lines follow, each line starts with a number N(1<=N<=100000), then N integers followed(all the integers are between -1000 and 1000).
```
### **Output**
```
For each test case, you should output two lines. The first line is "Case #:", # means the number of the test case. The second line contains three integers, the Max Sum in the sequence, the start position of the sub-sequence, the end position of the sub-sequence. If there are more than one result, output the first one. Output a blank line between two cases.
```
### **Sample Input**

```
2
5 6 -1 5 4 -7
7 0 6 -1 1 -6 7 -5
```

### **Sample Output**

```
Case 1:
14 1 4

Case 2:
7 1 6
```

### Notes
```
**动态规划**：①从第一个数字开始求和，如果加到某一个位置，和变成**负**的(即**对之后的求和无增益**)，起始点变更为这个位置的下一个位置，再从零开始求和。②每加一个数就立即与 $maxSum$ 比较动态调整左右边界。
```
### Code

```c++
#include <iostream>
#include "algorithm"
#include "cstdio"

using namespace std;


int main() {
    int T{};
    cin >> T;
    for(int t=1; t<=T; ++t){
        int n {};
        cin >> n;
        int left = 1;
        int maxSum = INT_MIN;
        int sum = 0;
        int start;
        int end;
        for(int i=1; i<=n; ++i){
            int num;
            cin >> num;
            sum += num;
            if(sum>maxSum){
                maxSum = sum;
                start = left;
                end = i;
            }
            if(sum<0){
                sum = 0;
                left = i + 1;
            }
        }
        printf("Case %d:\n", t);
        cout << maxSum << " " << start << " " << end << endl;
        if(t!=T) cout << endl;
    }
    return 0;
}
```

