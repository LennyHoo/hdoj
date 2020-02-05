# 1115 Lifting the Stone

### **Problem Description**

```
There are many secret openings in the floor which are covered by a big heavy stone. 
When the stone is lifted up, a special mechanism detects this and activates poisoned 
arrows that are shot near the opening. The only possibility is to lift the stone very 
slowly and carefully. The ACM team must connect a rope to the stone and then lift it 
using a pulley. Moreover, the stone must be lifted all at once; no side can rise 
before another. So it is very important to find the centre of gravity and connect the 
rope exactly to that point. The stone has a polygonal shape and its height is the same 
throughout the whole polygonal area. Your task is to find the centre of gravity for 
the given polygon.
```

### **Input**

```
The input consists of T test cases. The number of them (T) is given on the first line 
of the input file. Each test case begins with a line containing a single integer N (3 
<= N <= 1000000) indicating the number of points that form the polygon. This is 
followed by N lines, each containing two integers Xi and Yi (|Xi|, |Yi| <= 20000). 
These numbers are the coordinates of the i-th point. When we connect the points in the 
given order, we get a polygon. You may assume that the edges never touch each other 
(except the neighboring ones) and that they never cross. The area of the polygon is 
never zero, i.e. it cannot collapse into a single line.
```

### **Output**

```
Print exactly one line for each test case. The line should contain exactly two numbers 
separated by one space. These numbers are the coordinates of the centre of gravity. 
Round the coordinates to the nearest number with exactly two digits after the decimal 
point (0.005 rounds up to 0.01). Note that the centre of gravity may be outside the 
polygon, if its shape is not convex. If there is such a case in the input data, print 
the centre anyway.
```

### **Sample Input**

```
2
4
5 0
0 5
-5 0
0 -5
4
1 1
11 1
11 11
1 11
```

### **Sample Output**

```
0.00 0.00
6.00 6.00
```

### Notes

```C++
已知三点坐标，计算三角形面积的公式：
	double theArea(const Point &a, const Point &b, const Point &c){
    	return 0.5*(( b.x-a.x )*( c.y-a.y )-( c.x-a.x )*( b.y-a.y ));
	}
n边形质心的求解：
    分成 n-2 个三角形，质心各方向坐标是每个三角形质心在这个方向对面积的加权平均，详见代码。
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;

struct Point{
    double x;
    double y;
};


double theArea(const Point &a, const Point &b, const Point &c){
    return 0.5*(( b.x-a.x )*( c.y-a.y )-( c.x-a.x )*( b.y-a.y ));
}

int main(){
    int t;
    cin >> t;
    while(t--){
        int n;
        cin >> n;
        Point p0{}, p1{}, p2{};
        double areaSum = 0;
        double xSum = 0;
        double ySum = 0;
        cin >> p0.x >> p0.y;
        cin >> p1.x >> p1.y;
        for(int i=2; i<n; ++i){
            cin >> p2.x >> p2.y;
            double area = theArea(p0, p1, p2);
            xSum += (p0.x + p1.x + p2.x)*area;
            ySum += (p0.y + p1.y + p2.y)*area;
            areaSum += area;
            p1 = p2;
        }
        double Gx = xSum/areaSum/3+0.001;
        double Gy = ySum/areaSum/3+0.001;
        printf("%.2lf %.2lf\n", Gx, Gy);
    }
    return 0;
}
```

