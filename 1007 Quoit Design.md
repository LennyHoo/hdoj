# 1007 Quoit Design

### **Problem Description**

```
Have you ever played quoit in a playground? Quoit is a game in which flat rings are pitched at some toys, with all the toys encircled awarded.
In the field of Cyberground, the position of each toy is fixed, and the ring is carefully designed so it can only encircle one toy at a time. On the other hand, to make the game look more attractive, the ring is designed to have the largest radius. Given a configuration of the field, you are supposed to find the radius of such a ring.

Assume that all the toys are points on a plane. A point is encircled by the ring if the distance between the point and the center of the ring is strictly less than the radius of the ring. If two toys are placed at the same point, the radius of the ring is considered to be 0.
```

### **Input**

```
The input consists of several test cases. For each case, the first line contains an integer N (2 <= N <= 100,000), the total number of toys in the field. Then N lines follow, each contains a pair of (x, y) which are the coordinates of a toy. The input is terminated by N = 0.
```

### **Output**

```
For each test case, print in one line the radius of the ring required by the Cyberground manager, accurate up to 2 decimal places.
```

### **Sample Input**

```
2
0 0
1 1
2
1 1
1 1
3
-1.5 0
0 0
0 1.5
0
```

### **Sample Output**

```
0.71
0.00
0.75
```

### Notes

```
分治法：序列排序后，最小半径的两个端点有三种情况：都在 mid 左边，都在 mid 右边， 一个在左边且另一个在右边。
```

### Code

```C++
#include "iostream"
#include "cstdio"
#include "vector"
#include "cfloat"
#include "cmath"
#include "algorithm"

using namespace std;

class Node{
public:
    double first{};
    double second{};
public:
    Node(double first=0.f, double second=0.f){
        this->first = first;
        this->second = second;
    }
    bool operator < (const Node &a) const{
       if(this->first==a.first)
           return this->second<a.second;
       else return this->first<a.first;
    }
};


double D(Node a, Node b){
    return pow(a.first-b.first, 2)+pow(a.second-b.second, 2);
}

Node toys[100005];

double minD(int left, int right){
    if(right==left+1)    return D(toys[left], toys[right]);
    if(left==right) return INFINITY;
    int mid = (left+right)>>1;
    double leftRes = minD(left, mid);
    double rightRes = minD(mid+1, right);
    double res = min(leftRes, rightRes);
    for(int i=mid; i>=left&&toys[mid].first-toys[i].first<=res; --i){
        for(int j=mid+1; j<=right&&toys[j].first-toys[mid].first<=res; ++j){
            if(toys[j].second-toys[mid].second>res)   break;
            res = min(res, D(toys[i], toys[j]));
        }
    }
    return res;
}

int main(){
    while(true){
        int n{};
        scanf("%d", &n);
        if(!n)  return 0;
        for(int i=1; i<=n; ++i){
            double x, y;
            scanf("%lf %lf", &toys[i].first, &toys[i].second);
        }
        sort(toys+1, toys+n+1);
        double ans = sqrt(minD(1, n))/2;
        printf("%.2lf\n", ans);
    }
    return 0;
}
```

