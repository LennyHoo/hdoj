# 1004 Let the Balloon Rise

### **Problem Description**
```
Contest time again! How excited it is to see balloons floating around. But to tell you a secret, the judges' favorite time is guessing the most popular problem. When the contest is over, they will count the balloons of each color and find the result.

This year, they decide to leave this lovely job to you.
```
### **Input**
```
Input contains multiple test cases. Each test case starts with a number N (0 < N <= 1000) -- the total number of balloons distributed. The next N lines contain one color each. The color of a balloon is a string of up to 15 lower-case letters.

A test case with N = 0 terminates the input and this test case is not to be processed.
```
### **Output**
```
For each case, print the color of balloon for the most popular problem on a single line. It is guaranteed that there is a unique solution for each test case.
```
### **Sample Input**

```
5
green
red
blue
red
red
3
pink
orange
pink
0
```

### **Sample Output**

```
red
pink
```

### Notes
```
**哈希表：**建立一个存储有序对 **<Balloon_t, Times>** 的哈希表。每次输入一个气球的颜色，就在哈希表中查找，如果找不到就在表中添加一个记录；如果找到了，就在让这个颜色的出现次数加一。每次对哈希表修改，就将那个颜色出现的次数与当前最大出现次数比较，**动态修改**出现次数最多的颜色类型。
```
### Code

```c++
#include <iostream>
#include "algorithm"
#include "cstdio"
#include "map"
#include "string"

using namespace std;


int main() {
    int n{};
    while(true){
        cin >> n;
        if(!n) return 0;
        map<string, int> table;
        string color;
        int maxTimes = INT_MIN;
        string mostBalloon;
        while(n--){
            cin >> color;
            auto it = table.find(color);
            if(it==table.end())
                table.insert(pair<string, int>(color, 1));
            else
                ++it->second;
            it = table.find(color);
            if(it->second>maxTimes){
                maxTimes = it->second;
                mostBalloon = it->first;
            }
        }
        cout << mostBalloon << endl;
    }
}
```

