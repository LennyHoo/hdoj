# 1019 Least Common Multiple

### **Problem Description**

```
The least common multiple (LCM) of a set of positive integers is the smallest positive integer which is divisible by all the numbers in the set. For example, the LCM of 5, 7 and 15 is 105.
```

### **Input**

```
Input will consist of multiple problem instances. The first line of the input will contain a single integer indicating the number of problem instances. Each instance will consist of a single line of the form m n1 n2 n3 ... nm where m is the number of integers in the set and n1 ... nm are the integers. All integers will be positive and lie within the range of a 32-bit integer.
```

### **Output**

```
For each problem instance, output a single line containing the corresponding LCM. All results will lie in the range of a 32-bit integer.
```

### **Sample Input**

```
2
3 5 7 15
6 4 10296 936 1287 792 1
```

### **Sample Output**

```
105
10296
```

### Notes

```
最大公因数的求法（辗转相除法）：
	有两整数a和b：
        ① a%b得余数c
        ② 若c=0，则b即为两数的最大公约数
        ③ 若c≠0，则a=b，b=c，再回去执行①
最小公倍数的求法：
	最小公倍数=两整数的乘积÷最大公约数
```

### Code

```c++
#include <iostream>
#include "cstdio"
#include "cstring"
#include "cstdint"

using namespace std;

int64_t gcd(int64_t a, int64_t b){
    return (a%b)?(gcd(b, a%b)):(b);
}

int64_t lcm(int64_t a, int64_t b){
    return (a*b)/gcd(a, b);
}

int main() {
    int t{};
    cin >> t;
    while(t--){
        int m{};
        cin >> m;
        int res{};
        for(int i=1; i<=m; ++i){
            int64_t n;
            cin >> n;
            if(i==1)
                res = n;
            else
                res = lcm(res, n);
        }
        cout << res << endl;
    }
    return 0;
}
```

