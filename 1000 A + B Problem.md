# 1000 A + B Problem

### **Problem Description**

```
Calculate A + B.
```

### **Input**

```
Each line will contain two integers *A* and *B*. Process to end of file.
```

### **Output**

```
For each case, output *A + B* in one line.
```

### **Sample Input**

```
1 1
```

### **Sample Output**

```
2
```

### Notes

```
注意输入输出的格式。
```

### Code

```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
	// write your code here
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNextInt()){
             System.out.println(scanner.nextInt() + scanner.nextInt());
        }
    }
}
```

