# 1041 Computer Transformation

### **Problem Description**

```
A sequence consisting of one digit, the number 1 is initially written into a computer. At each successive time step, the computer simultaneously tranforms each digit 0 into the sequence 1 0 and each digit 1 into the sequence 0 1. So, after the first time step, the sequence 0 1 is obtained; after the second, the sequence 1 0 0 1, after the third, the sequence 0 1 1 0 1 0 0 1 and so on.
```

### **Input**

```
Every input line contains one natural number n (0 < n ≤1000).
```

### **Output**

```
For each input n print the number of consecutive zeroes pairs that will appear in the sequence after n steps.
```

### **Sample Input**

```
2
3
```

### **Sample Output**

```
1
1
```

### Notes

```
找规律、大数乘法、大数加法。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

vector<int> multiply(vector<int> a, int b){
    reverse(a.begin(), a.end());
    for(int i=0; i<a.size(); ++i){
        a[i] *= b;
    }
    int forwardNum = 0;
    for(int i=0; i<a.size(); ++i){
        int sum = forwardNum + a[i];
        a[i] = sum%10;
        forwardNum = sum / 10;
    }
    while(forwardNum>0){
        a.push_back(forwardNum%10);
        forwardNum /= 10;
    }
    reverse(a.begin(), a.end());
    return a;
}

vector<int> plusNum(vector<int> a, int b){
    reverse(a.begin(), a.end());
    int sum = b + a[0];
    int forwardNum = sum/10;
    a[0] = sum % 10;
    int pointer = 1;
    while(forwardNum>0){
        if(pointer==a.size())
            a.push_back(forwardNum);
        else{
            sum = forwardNum + a[pointer];
            forwardNum = sum/10;
            a[pointer] = sum % 10;
            ++pointer;
        }
    }
    reverse(a.begin(), a.end());
    return a;
}

int main() {
    int n{};
    while(cin>>n){
        vector<int> res(1, 0);
        for(int i=2; i<=n; ++i){
            if(i%2)
                res = plusNum(multiply(res, 2), -1);
            else
                res = plusNum(multiply(res, 2), 1);
        }
        for(auto c: res)
            printf("%d", c);
        printf("\n");
    }
    return 0;
}
```

