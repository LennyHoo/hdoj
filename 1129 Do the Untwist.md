# 1129 Do the Untwist

### Problem Description

```
http://acm.hdu.edu.cn/showproblem.php?pid=1129
```

### Notes

```
按照题意逆推即可。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

int charToInt(const char &c){
    if(c=='_')  return 0;
    if(c=='.')  return 27;
    return (c-'a'+1);
}

char intToChar(const int &n){
    if(n==0)    return '_';
    if(n==27)   return '.';
    return ('a'+n-1);
}

int MOD(int x, int y){
    return (x%y+y)%y;
}

int main()
{
    while(true){
        int key;
        cin >> key;
        if(!key) return 0;
        string ciphertext;
        cin >> ciphertext;
        int n = ciphertext.size();
        string plaintext(n, '0');
        for(int i=0; i<n; ++i){
            int ciphercode = charToInt(ciphertext[i]);
            int pos = MOD(key*i, n);
            int plaincode = ciphercode + i;
            if(plaincode>=28)
                plaincode %= 28;
            plaintext[pos] = intToChar(plaincode);
        }
        cout << plaintext << endl;
    }
    return 0;
}
```

