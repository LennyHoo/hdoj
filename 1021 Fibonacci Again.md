## 1021 Fibonacci Again

#### **Problem Description**

​		There are another kind of Fibonacci numbers: F(0) = 7, F(1) = 11, F(n) = F(n-1) + F(n-2) (n>=2).

#### **Input**

​		Input consists of a sequence of lines, each containing an integer n. (n < 1,000,000).

#### **Output**

​		Print the word "yes" if 3 divide evenly into F(n).

​		Print the word "no" if not.

#### **Sample Input**

```
0
1
2
3
4
5
```

#### **Sample Output**

```
no
no
yes
no
no
no
```

#### Notes

​		**两数之和与这两个数各自的余数之和同余**。

​		例如，在本题中：
$$
(a+b)\%3 = ((a\%3) + (b\%3))\%3
$$

#### Code

```c++
#include <iostream>
#include "cstdio"

using namespace std;


int main() {
    int n;
    while(cin >> n){
        int *dp = new int[n+1];
        dp[0] = 7 % 3;
        dp[1] = 11 % 3;
        for(int i=2; i<=n; ++i){
            dp[i] = (dp[i-1] + dp[i-2])%3;
        }
        bool res = !dp[n];
        if(res)
            cout << "yes" << endl;
        else
            cout << "no" << endl;
        delete[] dp;
    }
}
```

