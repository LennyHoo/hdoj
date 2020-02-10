# 1006 Tick and Tick

### **Problem Description**

```
The three hands of the clock are rotating every second and meeting each other many times everyday. Finally, they get bored of this and each of them would like to stay away from the other two. A hand is happy if it is at least D degrees from any of the rest. You are to calculate how much time in a day that all the hands are happy.
```

### **Input**

```
The input contains many test cases. Each of them has a single line with a real number D between 0 and 120, inclusively. The input is terminated with a D of -1.
```

### **Output**

```
For each D, print in a single line the percentage of time in a day that all of the hands are happy, accurate up to 3 decimal places.
```

### **Sample Input**

```
0
120
90
-1
```

### **Sample Output**

```
100.000
0.000
6.251
```

### Notes

```
模拟法。
```

### Code

```c++
#include<bits/stdc++.h>

using namespace std;

double max(double a,double b,double c){
    double result = a>b?a:b;
    result = result>c?result:c;
    return result;
}


double min(double a,double b,double c){

    double result = a<b?a:b;

    result = result<c?result:c;

    return result;

}


int main(){
    double angle;
    while(cin>>angle&&angle!=-1){
        double vsh,vsm,vmh,tsh,tsm,tmh,start,end,total=0;
        vsm = 6.-1./10.;vsh = 6.0-1./120.;vmh = 1./10.-1./120.;
        tsm = 360.0/vsm;tsh = 360.0/vsh;tmh = 360.0/vmh;
        double bsh,esh,bsm,esm,bmh,emh;
        bsh = angle/vsh;esh = (360.-angle)/vsh;
        bsm = angle/vsm;esm = (360.-angle)/vsm;
        bmh = angle/vmh;emh = (360.-angle)/vmh;
        while(bmh<43200){
            while(bsm<emh){
                while(bsh<emh&&bsh<esm){
                    start = max(bsh,bsm,bmh);
                    end = min(esh,esm,emh);
                    total += (end-start)>0?(end-start):0;
                    bsh = bsh+tsh;esh = esh+tsh;
                }
                bsh = bsh-tsh;esh = esh-tsh;
                bsm = bsm+tsm;esm = esm+tsm;
            }
            bsm = bsm-tsm;esm = esm-tsm;
            bmh = bmh+tmh;emh = emh+tmh;
        }
        cout<<fixed<<setprecision(3)<<total/432<<endl;}
    return 0;
}
```



