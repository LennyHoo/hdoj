# 1195 Open the Lock

### **Problem Description**

```
Now an emergent task for you is to open a password lock. The password is consisted of 
four digits. Each digit is numbered from 1 to 9.
Each time, you can add or minus 1 to any digit. When add 1 to '9', the digit will 
change to be '1' and when minus 1 to '1', the digit will change to be '9'. You can 
also exchange the digit with its neighbor. Each action will take one step.

Now your task is to use minimal steps to open the lock.

Note: The leftmost digit is not the neighbor of the rightmost digit.
```

### **Input**

```
The input file begins with an integer T, indicating the number of test cases.

Each test case begins with a four digit N, indicating the initial state of the 
password lock. Then followed a line with anotther four dight M, indicating the 
password which can open the lock. There is one blank line after each test case.
```

### **Output**

```
For each test case, print the minimal steps in one line.
```

### **Sample Input**

```
2
1234
2144

1111
9999
```

### **Sample Output**

```
2
4
```

### Notes

```
bfs
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;


string password;
bool visited[10005];
int d[] = {1, -1};


struct Node{
    int step{};
    string s;
    explicit Node() = default;
    explicit Node(int step, const string &s){
        this->step = step;
        this->s = s;
    }
};

string change(string s, int i, int j){
    swap(s[i], s[j]);
    return s;
}

string plusD(string s, int pos, int delta){
    s[pos] += delta;
    if(s[pos]=='9'+1)   s[pos] = '1';
    if(s[pos]=='1'-1)   s[pos] = '9';
    return s;
}

int bfs(const string &lock){
    if(lock==password)  return 0;
    memset(visited, false, sizeof(visited));
    queue<Node> Q;
    int num = (lock[0]-'0')*1000+(lock[1]-'0')*100+(lock[2]-'0')*10+(lock[3]-'0');
    visited[num] = true;
    Q.push(Node(0, lock));
    while(!Q.empty()){
        Node node = Q.front();
        Q.pop();
        for(int i=0; i<3; ++i){
                string s = change(node.s, i, i+1);
                if(s==password)
                    return node.step+1;
                num = (s[0]-'0')*1000+(s[1]-'0')*100+(s[2]-'0')*10+(s[3]-'0');
                if(!visited[num]) {
                    Q.push(Node(node.step+1, s));
                    visited[num] = true;
                }
        }
        for(int i=0; i<4; ++i){
            for(int j=0; j<2; ++j){
                string s = plusD(node.s, i, d[j]);
                if(s==password)
                    return node.step+1;
                num = (s[0]-'0')*1000+(s[1]-'0')*100+(s[2]-'0')*10+(s[3]-'0');
                if(!visited[num]) {
                    Q.push(Node(node.step+1, s));
                    visited[num] = true;
                }
            }
        }
    }
    return -1;
}


int main(){
    int t;
    cin >> t;
    while(t--){
        string lock;
        cin >> lock >> password;
        cout << bfs(lock) << endl;
    }
    return 0;
}
```

