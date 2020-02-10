# 1164 Eddy's research I

### **Problem Description**

```
Eddy's interest is very extensive, recently he is interested in prime number. Eddy 
discover the all number owned can be divided into the multiply of prime number, but he 
can't write program, so Eddy has to ask intelligent you to help him, he asks you to 
write a program which can do the number to divided into the multiply of prime number 
factor .
```

### **Input**

```
The input will contain a number 1 < x<= 65535 per line representing the number of 
elements of the set.
```

### **Output**

```
You have to print a line in the output for each entry with the answer to the previous 
question.
```

### **Sample Input**

```
11
9412
```

### **Sample Output**

```
11
2*2*13*181
```

### Notes

```
如果一个数是素数的话，那么它就不是它前面所有数的倍数
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;


int main(){
    int n;
    while(cin>>n){
        while(n!=1){
            for(int i=2; i<=n; ++i){
                if(n%i==0){
                    n /= i;
                    if(n!=1){
                        cout << i << "*";
                        i = 1;
                    }
                    else
                        cout << i << endl;
                }
            }
        }
    }
    return 0;
}
```

