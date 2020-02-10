# 1023 Train Problem II

### **Problem Description**

```
As we all know the Train Problem I, the boss of the Ignatius Train Station want to know if all the trains come in strict-increasing order, how many orders that all the trains can get out of the railway.
```

### **Output**

```
For each test case, you should output how many ways that all the trains can get out of the railway.
```

### **Sample Input**

```
1
2
3
10
```

### **Sample Output**

```
1
2
5
16796
```

### Notes

```
卡特兰数+大数乘法和除法

一个有n个元素的栈，不同的出栈顺序共有 Catalan(n) 种。

Catalan(0) = Catalan(1) = 1
递推关系： Catalan(n) = Catalan(n-1)*(4*n-2)/(n+1)
```

### Code

```C++
import java.math.BigInteger;
import java.util.Scanner;

public class Main {

    public static BigInteger[] dp = new BigInteger[101];;
    public static void main(String[] args) {
	// write your code here
        Scanner scanner = new Scanner(System.in);
        dp[0] = BigInteger.valueOf(1);
        dp[1] = BigInteger.valueOf(1);
        for(int i=2; i<=100; ++i){
            BigInteger a = BigInteger.valueOf(4*i-2);
            BigInteger b = BigInteger.valueOf(i+1);
            dp[i] = dp[i-1].multiply(a).divide(b);
        }
        while(scanner.hasNext()){
            int n = scanner.nextInt();
            System.out.println(dp[n]);
        }
    }
}
```

