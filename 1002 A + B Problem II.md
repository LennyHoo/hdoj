# 1002 A + B Problem II

### **Problem Description**
```
I have a very simple problem for you. Given two integers A and B, your job is to calculate the Sum of A + B.
```
### **Input**
```
The first line of the input contains an integer T(1<=T<=20) which means the number of test cases. Then T lines follow, each line consists of two positive integers, A and B. Notice that the integers are very large, that means you should not process them by using 32-bit integer. You may assume the length of each integer will not exceed 1000.
```
### **Output**
```
For each test case, you should output two lines. The first line is "Case #:", # means the number of the test case. The second line is the an equation "A + B = Sum", Sum means the result of A + B. Note there are some spaces int the equation. Output a blank line between two test cases.
```
### **Sample Input**

```
2
1 2
112233445566778899 998877665544332211
```

### **Sample Output**

```
Case 1:
1 + 2 = 3

Case 2:
112233445566778899 + 998877665544332211 = 1111111111111111110
```

### Notes
```
大数加法：用字符串储存两个数字。先反转两个字符串，然后逐位相加并进位，最后反转。
```
### Code

```c++
#include <iostream>
#include "algorithm"
#include "cstdio"
#include "string"

using namespace std;

void swap(string &a, string &b){
    string temp = a;
    a = b;
    b = temp;
}


string add(string a, string b){
    // 确保 a 比 b 长
    if(a.length()<b.length())   swap(a, b);
    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());
    int remainNum = 0;
    for(int i=0; i<b.length(); ++i){
        int sum = remainNum + (a[i] - '0') + (b[i] - '0');
        a[i] = sum % 10 + '0';
        remainNum = sum / 10;
    }
    for(int i=b.length(); i<a.length(); ++i){
        int sum = (a[i] - '0') + remainNum;
        a[i] = sum % 10 + '0';
        remainNum = sum / 10;
    }
    if(remainNum)
        a = a + (char)(remainNum+'0');
    reverse(a.begin(), a.end());
    return a;
}

int main() {
    int T;
    cin >> T;
    for(int i=1; i<=T; ++i){
        string a, b;
        cin >> a >> b;
        string res =  add(a, b);
        printf("Case %d:\n", i);
        cout << a << " + " << b << " = " << res << endl;
        if(i!=T) cout << endl;
    }
    return 0;
}
```

