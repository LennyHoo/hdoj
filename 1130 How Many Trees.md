# 1130 How Many Trees?

### **Problem Description**

```
A binary search tree is a binary tree with root k such that any node v reachable from its left has label (v) <label (k) and any node w reachable from its right has label (w) > label (k). It is a search structure which can find a node with label x in O(n log n) average time, where n is the size of the tree (number of vertices).

Given a number n, can you tell how many different binary search trees may be constructed with a set of numbers of size n such that each element of the set will be associated to the label of exactly one node in a binary search tree?
```

### **Input**

```
The input will contain a number 1 <= i <= 100 per line representing the number of elements of the set.
```

### **Output**

```
You have to print a line in the output for each entry with the answer to the previous question.
```

### **Sample Input**

```
1
2
3
```

### **Sample Output**

```
1
2
5
```

### Notes

```
卡特兰数+大数乘法和除法

一个有n个元素的二叉搜索树，不同的形态有 Catalan(n) 种。

Catalan(0) = Catalan(1) = 1
递推关系： Catalan(n) = Catalan(n-1)*(4*n-2)/(n+1)
```

### Code

```java
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

