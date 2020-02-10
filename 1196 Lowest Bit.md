# 1196 Lowest Bit

### **Problem Description**

```
Given an positive integer A (1 <= A <= 100), output the lowest bit of A.

For example, given A = 26, we can write A in binary form as 11010, so the lowest bit of A is 10, so the output should be 2.

Another example goes like this: given A = 88, we can write A in binary form as 1011000, so the lowest bit of A is 1000, so the output should be 8.
```

### **Input**

```
Each line of input contains only an integer A (1 <= A <= 100). A line containing "0" indicates the end of input, and this line is not a part of the input data.
```

### **Output**

```
For each A in the input, output a line containing only its lowest bit.
```

### **Sample Input**

```
26
88
0
```

### **Sample Output**

```
2
8
```

### Notes

```
思路：除2取余经过k次到余数不为0，输出 pow(2, k)
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;


int main(){
    while(true){
        int n;
        cin >> n;
        if(!n)
            return 0;
        int res = 0;
        int k = 0;
        while(n!=0){
            if(!(n%2)){
                n /= 2;
                ++k;
            }
            else
                break;
        }
        cout << pow(2, k) << endl;
    }
    return 0;
}
```

