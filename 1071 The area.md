# 1071 The area

### **Problem Description**

```
Ignatius bought a land last week, but he didn't know the area of the land because the land is enclosed by a parabola and a straight line. The picture below shows the area. Now given all the intersectant points shows in the picture, can you tell Ignatius the area of the land?

Note: The point P1 in the picture is the vertex of the parabola.
```

### **Input**

```
The input contains several test cases. The first line of the input is a single integer T which is the number of test cases. T test cases follow.
Each test case contains three intersectant points which shows in the picture, they are given in the order of P1, P2, P3. Each point is described by two floating-point numbers X and Y(0.0<=X,Y<=1000.0).
```

### **Output**

```
For each test case, you should output the area of the land, the result should be rounded to 2 decimal places.
```

### **Sample Input**

```
Sample Input
2
5.000000 5.000000
0.000000 0.000000
10.000000 0.000000
10.000000 10.000000
1.000000 1.000000
14.000000 8.222222
```

### **Sample Output**

```
33.33
40.69
```

### Notes

```
积分推导面积公式。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;


int main(){
    int n;
    cin >> n;
    getchar();
    while(n--){
        double x1, y1, x2, y2, x3, y3;
        cin >> x1 >> y1 >> x2 >> y2 >> x3 >> y3;
        double a = (y2-y1)/((x2-x1)*(x2-x1));
        double b = -2*a*x1;
        double c = y1+a*x1*x1;
        double res;
        if(x2==x3)
            res = 0.f;
        else{
            double k = (y3-y2)/(x3-x2);
            double t = y2-(y3-y2)*x2/(x3-x2);
            res = a*x3*x3*x3/3.f+(b-k)*x3*x3/2.f+(c-t)*x3
                  -(a*x2*x2*x2/3.f+(b-k)*x2*x2/2.f+(c-t)*x2);
        }
        printf("%.2lf\n", res);
    }
    return 0;
}
```

