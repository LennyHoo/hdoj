# 1147 Pick-up sticks

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1147
```

### Notes

```
题意：找出扔完之后下面没有木棒的木棒。
```

### Code

```c++
#include "iostream"
#include "vector"
#include "cstdio"
#include "algorithm"

using namespace std;

struct Stick{
    double x1;
    double y1;
    double x2;
    double y2;
    double a;
    double b;
    double c;
    int index;
    explicit Stick(double x1, double y1, double x2, double y2, int index){
        this->x1 = x1;
        this->y1 = y1;
        this->x2 = x2;
        this->y2 = y2;
        a = y1 - y2;
        b = x2 - x1;
        c = (x1-x2)*y1 - (y1-y2)*x1;
        this->index = index;
    }
};

bool isCross(const Stick &p, const Stick &q){
    if((p.a*q.x1+p.b*q.y1+p.c)*(p.a*q.x2+p.b*q.y2+p.c)>0)
        return false;
    if((q.a*p.x1+q.b*p.y1+q.c)*(q.a*p.x2+q.b*p.y2+q.c)>0)
        return false;
    return true;
}



int main()
{
    while(true){
        int n;
        scanf("%d", &n);
        if(!n)  return 0;
        vector<Stick> sticks;
        for(int i=1; i<=n; ++i){
            double x1, y1, x2, y2;
            scanf("%lf %lf %lf %lf", &x1, &y1, &x2, &y2);
            Stick newStick = Stick(x1, y1, x2, y2, i);
            for(auto it=sticks.begin(); it!=sticks.end(); ++it){
                if(isCross(*it, newStick)){
                    sticks.erase(it--);
                }
            }
            sticks.emplace_back(newStick);
        }
        printf("Top sticks:");
        int len = sticks.size();
        for(int i=0; i<len-1; ++i)
            printf(" %d,", sticks[i].index);
        printf(" %d.\n", sticks[len-1].index);
    }
    return 0;
}
```

