# 1020 Encoding

### **Problem Description**

```
Given a string containing only 'A' - 'Z', we could encode it using the following method:

1. Each sub-string containing k same characters should be encoded to "kX" where "X" is the only character in this sub-string.

2. If the length of the sub-string is 1, '1' should be ignored.
```

### **Input**

```
The first line contains an integer N (1 <= N <= 100) which indicates the number of test cases. The next N lines contain N strings. Each string consists of only 'A' - 'Z' and the length is less than 10000.
```

### **Output**

```
For each test case, output the encoded string in a line.
```

### **Sample Input**

```
2
ABC
ABBCCC
```

### **Sample Output**

```
ABC
A2B3C
```

### Notes

```
水题...
```

### Code

```c++
#include <iostream>
#include "cstdio"
#include "cstring"

using namespace std;


int main() {
    int t{};
    cin >> t;
    while(t--){
        string inString{};
        cin >> inString;
        string res = "";
        for(int i=0; i<inString.length(); ){
            int pointer = i;
            while(i<inString.length()&&inString[i]==inString[pointer]) ++i;
            if(i-pointer==1)
                res += inString[pointer];
            else
                res += to_string(i-pointer) + inString[pointer];
        }
        cout << res << endl;
    }
    return 0;
}
```

