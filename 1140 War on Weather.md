# 1140 War on Weather

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1140
```

### Notes

```
立体几何：计算卫星到地球视线的最大长度和卫星到热带风暴的距离比较。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

#define PI 3.1415926

struct Satellite{
    double x;
    double y;
    double z;
    double d;
    explicit Satellite(double x=0.f, double y=0.f, double z=0.f){
        this->x = x;
        this->y = y;
        this->z = z;
        this->d = sqrt((x*x+y*y+z*z)-pow(20000/PI, 2));
    }
};

int main()
{
    while(true){
        int k, m;
        cin >> k >> m;
        if(!k&&!m)  return 0;
        vector<Satellite> satellites;
        double x, y, z;
        for(int i=0; i<k; ++i){
            cin >> x >> y >> z;
            satellites.emplace_back(Satellite(x, y, z));
        }
        int res = 0;
        for(int i=0; i<m; ++i){
            cin >> x >> y >> z;
            for(auto &satellite: satellites){
                double distance = 
                    sqrt(pow(x-satellite.x, 2)+pow(y-satellite.y, 2)+pow(z-satellite.z, 2));
                if(distance<=satellite.d){
                    ++res;
                    break;
                }
            }
        }
        printf("%d\n", res);
    }
    return 0;
}
```

