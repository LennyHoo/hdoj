# 1051 Wooden Sticks

### **Problem Description**

```
There is a pile of n wooden sticks. The length and weight of each stick are known in 
advance. The sticks are to be processed by a woodworking machine in one by one 
fashion. It needs some time, called setup time, for the machine to prepare processing 
a stick. The setup times are associated with cleaning operations and changing tools 
and shapes in the machine. The setup times of the woodworking machine are given as 
follows:

(a) The setup time for the first wooden stick is 1 minute.
(b) Right after processing a stick of length l and weight w , the machine will need 
no setup time for a stick of length l' and weight w' if l<=l' and w<=w'. Otherwise, 
it will need 1 minute for setup.

You are to find the minimum setup time to process a given pile of n wooden sticks. 
For example, if you have five sticks whose pairs of length and weight are (4,9), 
(5,2), (2,1), (3,5), and (1,4), then the minimum setup time should be 2 minutes since 
there is a sequence of pairs (1,4), (3,5), (4,9), (2,1), (5,2).
```

### **Input**

```
The input consists of T test cases. The number of test cases (T) is given in the first 
line of the input file. Each test case consists of two lines: The first line has an 
integer n , 1<=n<=5000, that represents the number of wooden sticks in the test case, 
and the second line contains n 2 positive integers l1, w1, l2, w2, ..., ln, wn, each 
of magnitude at most 10000 , where li and wi are the length and weight of the i th 
wooden stick, respectively. The 2n integers are delimited by one or more spaces.
```

### **Output**

```
The output should contain the minimum setup time in minutes, one per line.
```

### **Sample Input**

```
3 
5 
4 9 5 2 2 1 3 5 1 4 
3 
2 2 1 1 2 2 
3 
1 3 2 2 3 1
```

### **Sample Output**

```
2
1
3
```

### Notes

```c++
贪心：对木棒进行排序，排序规则是：
	bool cmp(const Stick &a, const Stick &b){
        if(a.length==b.length)
            return (a.weight<b.weight);
        else 
            return (a.length<b.length);
	}

当数组不为空，就遍历处理，满足条件的就拣出来加工，不满足的先留着，等之后满足条件了处理。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

struct Stick{
    int length;
    int weight;
};

bool cmp(const Stick &a, const Stick &b){
    if(a.length==b.length)
        return (a.weight<b.weight);
    else 
        return (a.length<b.length);
}

int main()
{
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        vector<Stick> sticks(n);
        for(int i=0; i<n; ++i){
            cin >> sticks[i].length >> sticks[i].weight;
        }
        sort(sticks.begin(), sticks.end(), cmp);
        Stick now;
        int res = 0;
        while(!sticks.empty()){
            now = *sticks.begin();
            sticks.erase(sticks.begin());
            ++res;
            for(auto it=sticks.begin(); it!=sticks.end(); ++it){
                if(it->length>=now.length&&it->weight>=now.weight){
                    now = *it;
                    sticks.erase(it);
                    --it;
                }
            }
        }
        cout << res << endl;
    }
    return 0;
}
```

