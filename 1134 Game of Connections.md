# 1134 Game of Connections

### **Problem Description**

```
This is a small but ancient game. You are supposed to write down the numbers 1, 2, 3, 
... , 2n - 1, 2n consecutively in clockwise order on the ground to form a circle, and 
then, to draw some straight line segments to connect them into number pairs. Every 
number must be connected to exactly one another. And, no two segments are allowed to 
intersect.

It's still a simple game, isn't it? But after you've written down the 2n numbers, can 
you tell me in how many different ways can you connect the numbers into pairs? Life is 
harder, right?
```

### **Input**

```
Each line of the input file will be a single positive number n, except the last line, 
which is a number -1. You may assume that 1 <= n <= 100.
```

### **Output**

```
For each n, print in a single line the number of ways to connect the 2n numbers into 
pairs.
```

### **Sample Input**

```
2
3
-1
```

### **Sample Output**

```
2
5
```

### Notes

```
卡特兰数
```

### Code

```Java
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
            if(n==-1) return;
            System.out.println(dp[n]);
        }
    }
}
```

