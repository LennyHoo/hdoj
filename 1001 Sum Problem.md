# 1001 Sum Problem

### **Problem Description**

```
Hey, welcome to HDOJ(Hangzhou Dianzi University Online Judge).
In this problem, your task is to calculate SUM(n) = 1 + 2 + 3 + ... + n.
```

### **Input**

```
The input will consist of a series of integers n, one integer per line.
```
### **Output**
```
For each case, output SUM(n) in one line, followed by a blank line. You may assume the result will be in the range of 32-bit signed integer.
```
### **Sample Input**
```
1 
100
```
### **Sample Output**
```
1 

5050
```
### Notes
```
水题，但是输入输出格式交待得不清晰很坑。
```
#### Code

```c++
#include <iostream>

using namespace std;

int main() {
    int n;
    while(cin>>n){
        int sum = 0;
        for(int i=1; i<=n; ++i)
            sum += i;
        cout << sum << endl << endl;
    }
    return 0;
}
```

