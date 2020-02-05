# 1165 Eddy's research II

### **Problem Description**

```
As is known, Ackermann function plays an important role in the sphere of theoretical 
computer science. However, in the other hand, the dramatic fast increasing pace of the 
function caused the value of Ackermann function hard to calcuate.
Ackermann function can be defined recursively as follows:

img

Now Eddy Gives you two numbers: m and n, your task is to compute the value of A(m,n) 
.This is so easy problem,If you slove this problem,you will receive a prize(Eddy will 
invite you to hdu restaurant to have supper).
```

### **Input**

```
Each line of the input will have two integers, namely m, n, where 0 < m < =3.
Note that when m<3, n can be any integer less than 1000000, while m=3, the value of n is restricted within 24.
Input is terminated by end of file.
```

### **Output**

```
For each value of m,n, print out the value of A(m,n).
```

### **Sample Input**

```
1 3
2 4
```

### **Sample Output**

```
5
11
```

### Notes

```
公式推导
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;

int A(int m, int n){
    if(m==0)
        return n+1;
    else if(m==1)
        return n+2;
    else if(m==2)
        return 2*n+3;
    else
        return pow(2, n+3)-3;
}

int main(){
    int m, n;
    while(cin>>m>>n){
        cout << A(m, n) << endl;
    }
    return 0;
}
```

