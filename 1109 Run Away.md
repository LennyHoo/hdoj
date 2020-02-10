# 1109 Run Away

### **Problem Description**

```
One of the traps we will encounter in the Pyramid is located in the Large Room. A lot 
of small holes are drilled into the floor. They look completely harmless at the first 
sight. But when activated, they start to throw out very hot java, uh ... pardon, lava. 
Unfortunately, all known paths to the Center Room (where the Sarcophagus is) contain a 
trigger that activates the trap. The ACM were not able to avoid that. But they have 
carefully monitored the positions of all the holes. So it is important to find the 
place in the Large Room that has the maximal distance from all the holes. This place 
is the safest in the entire room and the archaeologist has to hide there.
```

### **Input**

```
The input consists of T test cases. The number of them (T) is given on the first line 
of the input file. Each test case begins with a line containing three integers X, Y, M 
separated by space. The numbers satisfy conditions: 1 <= X,Y <=10000, 1 <= M <= 1000. 
The numbers X and Yindicate the dimensions of the Large Room which has a rectangular 
shape. The number M stands for the number of holes. Then exactly M lines follow, each 
containing two integer numbers Ui and Vi (0 <= Ui <= X, 0 <= Vi <= Y) indicating the 
coordinates of one hole. There may be several holes at the same position.
```

### **Output**

```
Print exactly one line for each test case. The line should contain the sentence "The 
safest point is (P, Q)." where P and Qare the coordinates of the point in the room 
that has the maximum distance from the nearest hole, rounded to the nearest number 
with exactly one digit after the decimal point (0.05 rounds up to 0.1).
```

### **Sample Input**

```
3
1000 50 1
10 10
100 100 4
10 10
10 90
90 10
90 90
3000 3000 4
1200 85
63 2500
2700 2650 
2990 100
```

### **Sample Output**

```
The safest point is (1000.0, 50.0).
The safest point is (50.0, 50.0).
The safest point is (1433.0, 1669.8).
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
double max_x, max_y;

double evaluate(const Node &res){
    double minLength = FLT_MAX;
    for(auto &node: nodes){
        double len = pow(res.x-node.x, 2)+pow(res.y-node.y, 2);
        if(len<minLength)
            minLength = len;
    }
    return -minLength;
}



Node SA(){
    // 初始化
    srand(rand());
    default_random_engine random(rand());
    uniform_real_distribution<double> tiny_x(-1, 1);
    uniform_real_distribution<double> tiny_y(-1, 1);
    Node res = Node(max_x/2.f, max_y/2.f);
    // 初始参数
    double T0 = 1e3;    // 初始温度
    double k = 0.9993;   // 降温系数
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
        cin >> max_x >> max_y >> n;
        nodes = vector<Node>(n);
        for(int i=0; i<n; ++i){
            cin >> nodes[i].x >> nodes[i].y;
        }
        Node res = SA();
        printf("The safest point is (%.1lf, %.1lf).\n", res.x, res.y);
    }
    return 0;
}
```

