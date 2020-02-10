# 1124 Factorial

### **Problem Description**

```
The most important part of a GSM network is so called Base Transceiver Station (BTS). 
These transceivers form the areas called cells (this term gave the name to the 
cellular phone) and every phone connects to the BTS with the strongest signal (in a 
little simplified view). Of course, BTSes need some attention and technicians need to 
check their function periodically.
ACM technicians faced a very interesting problem recently. Given a set of BTSes to 
visit, they needed to find the shortest path to visit all of the given points and 
return back to the central company building. Programmers have spent several months 
studying this problem but with no results. They were unable to find the solution fast 
enough. After a long time, one of the programmers found this problem in a conference 
article. Unfortunately, he found that the problem is so called "Travelling Salesman 
Problem" and it is very hard to solve. If we have N BTSes to be visited, we can visit 
them in any order, giving us N! possibilities to examine. The function expressing 
that number is called factorial and can be computed as a product 1.2.3.4....N. The 
number is very high even for a relatively small N.

The programmers understood they had no chance to solve the problem. But because they 
have already received the research grant from the government, they needed to continue 
with their studies and produce at least some results. So they started to study 
behaviour of the factorial function.

For example, they defined the function Z. For any positive integer N, Z(N) is the 
number of zeros at the end of the decimal form of number N!. They noticed that this 
function never decreases. If we have two numbers N1<N2, then Z(N1) <= Z(N2). It is 
because we can never "lose" any trailing zero by multiplying by any positive number. 
We can only get new and new zeros. The function Z is very interesting, so we need a 
computer program that can determine its value efficiently.
```

### **Input**

```
There is a single positive integer T on the first line of input. It stands for the 
number of numbers to follow. Then there is T lines, each containing exactly one 
positive integer number N, 1 <= N <= 1000000000.
```

### **Output**

```
For every number N, output a single line containing the single non-negative integer 
Z(N).
```

### **Sample Input**

```
6
3
60
100
1024
23456
8735373
```

### **Sample Output**

```
0
14
24
253
5861
2183837
```

### Notes

```
首先给出一个性质：

n!的素因子分解中的素数p的幂为：[ n / p ] + [ n / p² ] + [ n / p³ ] + ……

 
举例证明：

例如我们有10!，我们要求它的素因子分解中2的幂；

那么，根据公式有 [ 10 / 2 ] + [ 10 / 4 ] + [ 10 / 8 ] （后面例如[10/16]之类的都为0）；

显然[ 10 / 2 ] = 5，代表了从1~10中有几个数是2的倍数：2,4,6,8,10；它们每个数都为10!提供了1个2；

之后[ 10 / 4 ] = 2，代表了从1~10中有几个数是4的倍数：4,8；那加上这两个数是为什么呢？因为在前面已经提供了5个2的基础上，4和8可以各再多提供1个2；

[ 10 / 8 ] = 1，代表了从1~10中有几个数是8的倍数：8；因为同样的，在前面的基础上，8又可以再提供一个2；

这样，可以说这个公式为什么是这样的，已经很明显了；

10 必然由 2*5 提供， 显然 2 的因子数必然比 5 的因子数多，所以问题就演变成 n! 中有多少个5相乘。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


int main()
{
    int t;
    cin >> t;
    while(t--){
        int64_t n;
        cin >> n;
        int64_t factor = 5;
        int64_t res = 0;
        while(factor<=n){
            res += n/factor;
            factor *= 5;
        }
        cout << res << endl;
    }
    return 0;
}
```

