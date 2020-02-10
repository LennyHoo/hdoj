# 1009 FatMouse' Trade

### **Problem Description**

```
FatMouse prepared M pounds of cat food, ready to trade with the cats guarding the warehouse containing his favorite food, JavaBean.
The warehouse has N rooms. The i-th room contains J[i] pounds of JavaBeans and requires F[i] pounds of cat food. FatMouse does not have to trade for all the JavaBeans in the room, instead, he may get J[i]* a% pounds of JavaBeans if he pays F[i]* a% pounds of cat food. Here a is a real number. Now he is assigning this homework to you: tell him the maximum amount of JavaBeans he can obtain.
```

### **Input**

```
The input consists of multiple test cases. Each test case begins with a line containing two non-negative integers M and N. Then N lines follow, each contains two non-negative integers J[i] and F[i] respectively. The last test case is followed by two -1's. All integers are not greater than 1000.
```

### **Output**

```
For each test case, print in a single line a real number accurate up to 3 decimal places, which is the maximum amount of JavaBeans that FatMouse can obtain.
```

### **Sample Input**

```
5 3
7 2
4 3
5 2
20 3
25 18
24 15
15 10
-1 -1
```

### **Sample Output**

```
13.333
31.500
```

### Notes

```
贪心算法：将输入的数据以类型 Trade 的形式储存，按照 rate 从高到低排序，如果老鼠还有剩余的猫粮就优先选择收益率高的交易进行，直到老鼠的猫粮值变为负数。
```

### Code

```c++
#include <iostream>
#include "cstdio"
#include "cmath"
#include "vector"
#include "algorithm"

using namespace std;

class Trade{
public:
    double j;
    double f;
    double rate;
public:
    Trade(double j, double f){
        this->j = j;
        this->f = f;
        if(j)
            this->rate = f/j;
        else
            this->rate = -1;
    }
};

bool cmp(Trade a, Trade b){
    return a.rate>b.rate;
}


int main() {
    while(true){
        double m;
        int n;
        cin >> m >> n;
        if(m==-1&&n==-1)    return 0;
        vector<Trade> list;
        while(n--){
            double j, f;
            cin >> f >> j;
            list.emplace_back(j, f);
        }
        sort(list.begin(), list.end(), cmp);
        double get = 0;
        size_t i = 0;
        while(m>=0&&i<list.size()){
            double pay{};
            if(m>list[i].j)
                pay = list[i].j;
            else
                pay = m;
            if(list[i].rate!=-1)
                get += list[i].rate*pay;
            else
                get += list[i].f;
            m -= pay;
            ++i;
        }
        printf("%.3lf\n", get);
    }
}
```

