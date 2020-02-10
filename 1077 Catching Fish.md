# 1077 Catching Fish

### **Problem Description**

```
Ignatius likes catching fish very much. He has a fishnet whose shape is a circle of 
radius one. Now he is about to use his fishnet to catch fish. All the fish are in the 
lake, and we assume all the fish will not move when Ignatius catching them. Now 
Ignatius wants to know how many fish he can catch by using his fishnet once. We assume 
that the fish can be regard as a point. So now the problem is how many points can be 
enclosed by a circle of radius one.

Note: If a fish is just on the border of the fishnet, it is also caught by Ignatius.
```

### **Input**

```
The input contains several test cases. The first line of the input is a single integer 
T which is the number of test cases. T test cases follow.
Each test case starts with a positive integer N(1<=N<=300) which indicate the number 
of fish in the lake. Then N lines follow. Each line contains two floating-point number 
X and Y (0.0<=X,Y<=10.0). You may assume no two fish will at the same point, and no 
two fish are closer than 0.0001, no two fish in a test case are approximately at a 
distance of 2.0. In other words, if the distance between the fish and the centre of 
the fishnet is smaller 1.0001, we say the fish is also caught.
```

### **Output**

```
For each test case, you should output the maximum number of fish Ignatius can catch by 
using his fishnet once.
```

### **Sample Input**

```
4
3
6.47634 7.69628
5.16828 4.79915
6.69533 6.20378
6
7.15296 4.08328
6.50827 2.69466
5.91219 3.86661
5.29853 4.16097
6.10838 3.46039
6.34060 2.41599
8
7.90650 4.01746
4.10998 4.18354
4.67289 4.01887
6.33885 4.28388
4.98106 3.82728
5.12379 5.16473
7.84664 4.67693
4.02776 3.87990
20
6.65128 5.47490
6.42743 6.26189
6.35864 4.61611
6.59020 4.54228
4.43967 5.70059
4.38226 5.70536
5.50755 6.18163
7.41971 6.13668
6.71936 3.04496
5.61832 4.23857
5.99424 4.29328
5.60961 4.32998
6.82242 5.79683
5.44693 3.82724
6.70906 3.65736
7.89087 5.68000
6.23300 4.59530
5.92401 4.92329
6.24168 3.81389
6.22671 3.62210
```

### **Sample Output**

```
2
5
5
11
```

### Notes

```
模拟退火
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


struct Node{
    double x;
    double y;
    explicit Node(double x=0.f, double y=0.f){
        this->x = x;
        this->y = y;
    }
};


vector<Node> nodes;
double max_x = 10.f , max_y = 10.f;

int evaluate(const Node &res){
    int val = 0;
    for(auto &node: nodes){
        double len = pow(res.x-node.x, 2)+pow(res.y-node.y, 2);
        if(len<=1.f)
            ++val;
    }
    return -val;
}



Node SA(){
    // 初始化
    srand(rand());
    default_random_engine random(rand());
    uniform_real_distribution<double> tiny_x(-1, 1);
    uniform_real_distribution<double> tiny_y(-1, 1);
    Node res = Node(max_x/2.f, max_y/2.f);
    // 初始参数
    double T0 = 10;    // 初始温度
    double k = 0.99993;   // 降温系数
    double Tk = 1e-6;
    double T = T0;
    while(T>Tk) {
        Node changedNode = res;
        changedNode.x += tiny_x(random)*T;
        changedNode.y += tiny_y(random)*T;
        if(changedNode.x<0.f)   changedNode.x = 0.f;
        if(changedNode.y<0.f)   changedNode.y = 0.f;
        if(changedNode.x>max_x) changedNode.x = max_x;
        if(changedNode.y>max_y) changedNode.y = max_y;
        double diff = evaluate(changedNode) - evaluate(res);
        if (diff < 0)
            res = changedNode;
        else {
            if (exp(-diff / T) * RAND_MAX > rand())
                res = changedNode;
        }
        T *= k;
    }
    return res;
}



int main()
{
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        nodes = vector<Node>(n);
        for(int i=0; i<n; ++i){
            cin >> nodes[i].x >> nodes[i].y;
        }
        Node res = SA();
        printf("%d\n", -evaluate(res));
    }
    return 0;
}
```

