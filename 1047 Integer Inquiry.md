# 1047 Integer Inquiry

### **Problem Description**

```
One of the first users of BIT's new supercomputer was Chip Diller. He extended his exploration of powers of 3 to go from 0 to 333 and he explored taking various sums of those numbers.
``This supercomputer is great,'' remarked Chip. ``I only wish Timothy were here to see these results.'' (Chip moved to a new apartment, once one became available on the third floor of the Lemon Sky apartments on Third Street.)
```

### **Input**

```
The input will consist of at most 100 lines of text, each of which contains a single VeryLongInteger. Each VeryLongInteger will be 100 or fewer characters in length, and will only contain digits (no VeryLongInteger will be negative).

The final input line will contain a single zero on a line by itself.
```

### **Output**

```
Your program should output the sum of the VeryLongIntegers given in the input.


This problem contains multiple test cases!

The first line of a multiple input is an integer N, then a blank line followed by N input blocks. Each input block is in the format indicated in the problem description. There is a blank line between input blocks.

The output format consists of N output blocks. There is a blank line between output blocks.
```

### **Sample Input**

```
1


123456789012345678901234567890
123456789012345678901234567890
123456789012345678901234567890
0
```

### **Sample Output**

```
370370367037037036703703703670
```

### Notes

```
大数加法。
```

### Code

```c++
#include<bits/stdc++.h>

using namespace std;

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
    while(true){
        int n{};
        cin >> n;
        if(!n)
            return 0;
        for(int i=0; i<n; ++i){
            string res = "0";
            string num{};
            cin >> num;
            while(num!="0"){
                res = add(res, num);
                cin >> num;
            }
            cout << res << endl;
            if(i!=n-1)  cout << endl;
        }
    }
    return 0;
}
```

