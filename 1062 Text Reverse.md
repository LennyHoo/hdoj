# 1062 Text Reverse

### **Problem Description**

```
Ignatius likes to write words in reverse way. Given a single line of text which is written by Ignatius, you should reverse all the words and then output them.
```

### **Input**

```
The input contains several test cases. The first line of the input is a single integer T which is the number of test cases. T test cases follow.
Each test case contains a single line with several words. There will be at most 1000 characters in a line.
```

### **Output**

```
For each test case, you should output the text which is processed.
```

### **Sample Input**

```
3
olleh !dlrow
m'I morf .udh
I ekil .mca
```

### Sample Output

```
hello world!
I'm from hdu.
I like acm.
```

### Notes

```
双指针、用 getline() 获取输入。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;


int main(){
    int n;
    cin >> n;
    getchar();
    while(n--){
        string s;
        getline(cin, s);
        auto p = s.begin();
        auto q = p;
        while(q<s.end()){
            while(*q!=' '&&q!=s.end())  ++q;
            reverse(p, q);
            p = q + 1;
            q = p;
        }
        cout << s << endl;
    }
    return 0;
}
```

