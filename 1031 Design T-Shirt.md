# 1031 Design T-Shirt

### **Problem Description**

```
Soon after he decided to design a T-shirt for our Algorithm Board on Free-City BBS, XKA found that he was trapped by all kinds of suggestions from everyone on the board. It is indeed a mission-impossible to have everybody perfectly satisfied. So he took a poll to collect people's opinions. Here are what he obtained: N people voted for M design elements (such as the ACM-ICPC logo, big names in computer science, well-known graphs, etc.). Everyone assigned each element a number of satisfaction. However, XKA can only put K (<=M) elements into his design. He needs you to pick for him the K elements such that the total number of satisfaction is maximized.
```

### **Input**

```
The input consists of multiple test cases. For each case, the first line contains three positive integers N, M and K where N is the number of people, M is the number of design elements, and K is the number of elements XKA will put into his design. Then N lines follow, each contains M numbers. The j-th number in the i-th line represents the i-th person's satisfaction on the j-th element.
```

### **Output**

```
For each test case, print in one line the indices of the K elements you would suggest XKA to take into consideration so that the total number of satisfaction is maximized. If there are more than one solutions, you must output the one with minimal indices. The indices start from 1 and must be printed in non-increasing order. There must be exactly one space between two adjacent indices, and no extra space at the end of the line.
```

### **Sample Input**

```
3 6 4
2 2.5 5 1 3 4
5 1 3.5 2 2 2
1 1 1 1 1 10
3 3 2
1 2 3
2 3 1
3 1 2
```

### **Sample Output**

```
6 5 3 1
2 1
```

### Notes

```
水题，记得索引值也要按从大到小排序。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

class Elem{
public:
    int index{};
    double value{};
public:
    Elem(int index, double value){
        this->index = index;
        this->value = value;
    }
    bool operator<(const Elem &e){
        return this->value>e.value;
    }
};


int main(){
    int n, m, k;
    while(cin>>n>>m>>k){
        vector<Elem> elements;
        for(int i=1; i<=m; ++i){
            double value{};
            cin >> value;
            elements.emplace_back(Elem(i, value));
        }
        for(int i=1; i<n; ++i){
            for(int j=0; j<m; ++j){
                double value{};
                cin >> value;
                elements[j].value += value;
            }
        }
        sort(elements.begin(), elements.end());
        vector<int> indexRes;
        for(int i=0; i<k; ++i)
            indexRes.push_back(elements[i].index);
        sort(indexRes.begin(), indexRes.end());
        for(int i=indexRes.size()-1; i>=1; --i)
            printf("%d ", indexRes[i]);
        printf("%d\n", indexRes[0]);
    }
    return 0;
}
```

