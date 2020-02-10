# 1200 To and Fro

### **Problem Description**

```
Mo and Larry have devised a way of encrypting messages. They first decide secretly on the number of columns and write the message (letters only) down the columns, padding with extra random letters so as to make a rectangular array of letters. For example, if the message is “There’s no place like home on a snowy night” and there are five columns, Mo would write down

t o i o y
h p k n n
e l e a i
r a h s g
e c o n h
s e m o t
n l e w x


Note that Mo includes only letters and writes them all in lower case. In this example, Mo used the character ‘x’ to pad the message out to make a rectangle, although he could have used any letter.

Mo then sends the message to Larry by writing the letters in each row, alternating left-to-right and right-to-left. So, the above would be encrypted as

toioynnkpheleaigshareconhtomesnlewx

Your job is to recover for Larry the original message (along with any extra padding letters) from the encrypted one.
```

### **Input**

```
There will be multiple input sets. Input for each set will consist of two lines. The 
first line will contain an integer in the range 2. . . 20 indicating the
```

### **Output**

```
Each input set should generate one line of output, giving the original plaintext 
message, with no spaces.
```

### **Sample Input**

```
5
toioynnkpheleaigshareconhtomesnlewx
3
ttyohhieneesiaabss
0
```

### **Sample Output**

```
theresnoplacelikehomeonasnowynightx
thisistheeasyoneab
```

### Notes

```
暴力模拟
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


int main()
{
    while(true){
        int n;
        cin >> n;
        if(!n)  return 0;
        string s;
        cin >> s;
        int m = ceil(s.size()/n);
        vector<vector<char>> grid(m, vector<char>(n));
        int row = 0;
        int col = 0;
        int pos = 0;
        bool toRight = true; 
        while(row<m&&pos<s.size()){
            grid[row][col] = s[pos];
            ++pos;
            if(toRight){
                if(col<n-1) ++col;
                else  {
                    toRight = false;
                    ++row;
                }  
            }
            else{
                if(col>0)   --col;
                else {
                    toRight = true;
                    ++row;
                }
            }
        }
        string res = "";
        for(int j=0; j<n; ++j){
            for(int i=0; i<m; ++i){
                res += grid[i][j];
            }
        }
        cout << res << endl;
    }
    return 0;
}
```

