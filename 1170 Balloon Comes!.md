# 1170 Balloon Comes!

### **Problem Description**

```
The contest starts now! How excited it is to see balloons floating around. You, one of 
the best programmers in HDU, can get a very beautiful balloon if only you have solved 
the very very very... easy problem.
Give you an operator (+,-,*, / --denoting addition, subtraction, multiplication, 
division respectively) and two positive integers, your task is to output the result.
Is it very easy?
Come on, guy! PLMM will send you a beautiful Balloon right now!
Good Luck!
```

### **Input**

```
Input contains multiple test cases. The first line of the input is a single integer T 
(0<T<1000) which is the number of test cases. T test cases follow. Each test case 
contains a char C (+,-,*, /) and two integers A and B(0<A,B<10000).Of course, we all 
know that A and B are operands and C is an operator.
```

### **Output**

```
For each case, print the operation result. The result should be rounded to 2 decimal 
places If and only if it is not an integer.
```

### **Sample Input**

```
4
+ 1 2
- 1 2
* 1 2
/ 1 2
```

### **Sample Output**

```
3
-1
2
0.50
```

### Notes

```
水题
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


int main()
{
    int n;
    cin >> n;
    while(n--){
        char c;
        int a, b;
        cin >> c >> a >> b;
        switch(c){
            case '+':
                printf("%d\n", a+b);   break;
            case '-':
                printf("%d\n", a-b);    break;
            case '*':
                printf("%d\n", a*b);    break;
            case '/':
                if(a%b)
                    printf("%.2lf\n", a*1.f/b);
                else 
                    printf("%d\n", a/b);
        }
    }
    return 0;
}
```

