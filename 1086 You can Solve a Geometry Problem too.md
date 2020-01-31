# 1086 You can Solve a Geometry Problem too

### **Problem Description**

```
Many geometry（几何）problems were designed in the ACM/ICPC. And now, I also prepare a geometry problem for this final exam. According to the experience of many ACMers, geometry problems are always much trouble, but this problem is very easy, after all we are now attending an exam, not a contest :)
Give you N (1<=N<=100) segments（线段）, please output the number of all intersections（交点）. You should count repeatedly if M (M>2) segments intersect at the same point.

Note:
You can assume that two segments would not intersect at more than one point.
```

### **Input**

```
Input contains multiple test cases. Each test case contains a integer N (1=N<=100) in a line first, and then N lines follow. Each line describes one segment with four float values x1, y1, x2, y2 which are coordinates of the segment’s ending.
A test case starting with 0 terminates the input and this test case is not to be processed.
```

### **Output**

```
For each case, print the number of intersections, and one line one case.
```

### **Sample Input**

```
2
0.00 0.00 1.00 1.00
0.00 1.00 1.00 0.00
3
0.00 0.00 1.00 1.00
0.00 1.00 1.00 0.000
0.00 0.00 1.00 0.00
0
```

### **Sample Output**

```
1
3
```

### Notes

```
已知：由点A和点B组成的线段1，由点C和点D组成的线段2
方法：当点A和点B在线段2的两侧，并且点C和点D在线段1的两侧时，两线段相交，否则不相交
判断两点是否在线段同侧的方法，根据简单线性规划，只限本将二维平面分成两部分，平面的点，一部分的值大于0，一部分的值小于0，所以两点带入直线时所得值之积大于0时在同侧，小于0时在两侧。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

class Line{
public:
    double x1{};
    double y1{};
    double x2{};
    double y2{};
    double k{};
    double b{};
public:
    Line(){

    }
    Line(double x1, double y1, double x2, double y2){
        this->x1 = x1;
        this->y1 = y1;
        this->x2 = x2;
        this->y2 = y2;
        if(x1!=x2){
            this->k = (y1-y2)/(x1-x2);
            this->b = y1 - this->k*x1;
        }
        else
            this->k = FLT_MAX;
    }
};

bool helper(const Line &a, const Line &b){
    if(a.x1==a.x2){
        if((b.x1-a.x1)*(b.x2-a.x2)>0)
            return false;
    }
    else{
        if((a.k*b.x1-b.y1+a.b)*(a.k*b.x2-b.y2+a.b)>0)
            return false;
    }
    if(b.x1==b.x2){
        if((a.x1-b.x1)*(a.x2-b.x2)>0)
            return false;
    }
    else{
        if((b.k*a.x1-a.y1+b.b)*(b.k*a.x2-a.y2+b.b)>0)
            return false;
    }
    return true;
}

int main(){
    while(true){
        int n;
        cin >> n;
        if(!n)  return 0;
        vector<Line> lines;
        int res = 0;
        for(int i=0; i<n; ++i){
            double x1, y1, x2, y2;
            cin >> x1 >> y1 >> x2 >> y2;
            lines.emplace_back(Line(x1, y1, x2, y2));
            for(int j=i-1; j>=0; --j){
                if(helper(lines[i], lines[j]))
                    ++res;
            }
        }
        cout << res << endl;
    }
    return 0;
}
```

