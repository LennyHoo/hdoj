# 1104 Remainder

### **Problem Description**

```
Coco is a clever boy, who is good at mathematics. However, he is puzzled by a 
difficult mathematics problem. The problem is: Given three integers N, K and M, N may 
adds (‘+’) M, subtract (‘-‘) M, multiples (‘*’) M or modulus (‘%’) M (The definition 
of ‘%’ is given below), and the result will be restored in N. Continue the process 
above, can you make a situation that “[(the initial value of N) + 1] % K” is equal to 
“(the current value of N) % K”? If you can, find the minimum steps and what you should 
do in each step. Please help poor Coco to solve this problem.

You should know that if a = b * q + r (q > 0 and 0 <= r < q), then we have a % q = r.
```

### **Input**

```
There are multiple cases. Each case contains three integers N, K and M (-1000 <= N <= 
1000, 1 < K <= 1000, 0 < M <= 1000) in a single line.

The input is terminated with three 0s. This test case is not to be processed.
```

### **Output**

```
For each case, if there is no solution, just print 0. Otherwise, on the first line of 
the output print the minimum number of steps to make “[(the initial value of N) + 1] % 
K” is equal to “(the final value of N) % K”. The second line print the operations to 
do in each step, which consist of ‘+’, ‘-‘, ‘*’ and ‘%’. If there are more than one 
solution, print the minimum one. (Here we define ‘+’ < ‘-‘ < ‘*’ < ‘%’. And if A = 
a1a2...ak and B = b1b2...bk are both solutions, we say A < B, if and only if there 
exists a P such that for i = 1, ..., P-1, ai = bi, and for i = P, ai < bi)
```

### **Sample Input**

```
2 2 2
-1 12 10
0 0 0
```

### **Sample Output**

```
0
2
*+
```

### Notes

```
本题中的 % 结果都是非负数，所以要重定义一个 MOD；
为了避免溢出，每次求的数都 MOD m*k；
为什么要 MOD m*k？

	因为对于N来说，其中的过程会有N+m,N-m,以及N*m,按照正常的步骤来说，统一%K，但是因为有N%m的插足，
例如： (N+m-m*m%m)%k  （从左到右依次执行，没有优先级）
            (N%k+m%k-m%k*m%k%m%k)%k这两个是绝对不相等的
但是统一%mk是相等的，因为你%mk，是对所有的（）里的数进行的，而第二个式子中因为对除最后一个数外进行的事%mk，而其他数进行的仅是%k所以不相等。
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

struct Node{
    int x;
    int step;
    string path;
    explicit Node(int x, int step=0, string path=""){
        this->x = x;
        this->step = step;
        this->path = path;
    }
};

int MOD(int x, int y){
    return (x%y + y)%y;
}

int n, k, m;
map<int, int> vis;

pair<int, string> bfs(){
    queue<Node> Q;
    Node start(n);
    int code = 0;
    Q.push(start);
    vis.clear();
    vis.insert(make_pair(n, code++));
    while(!Q.empty()){
        Node node = Q.front();
        Q.pop();
        int newNum = MOD(node.x + m, m*k);
        if(MOD(newNum, k)==MOD(n+1, k))
            return make_pair(node.step+1, node.path+"+");
        if(vis.find(newNum)==vis.end()){
            Q.push(Node(newNum, node.step+1, node.path+"+"));
            vis.insert(make_pair(newNum, code++));
        }
        newNum = MOD(node.x-m, m*k);
        if(MOD(newNum, k)==MOD(n+1, k))
            return make_pair(node.step+1, node.path+"-");
        if(vis.find(newNum)==vis.end()){
            Q.push(Node(newNum, node.step+1, node.path+"-"));
            vis.insert(make_pair(newNum, code++));
        }
        newNum = MOD(node.x*m, m*k);
        if(MOD(newNum, k)==MOD(n+1, k))
            return make_pair(node.step+1, node.path+"*");
        if(vis.find(newNum)==vis.end()){
            Q.push(Node(newNum, node.step+1, node.path+"*"));
            vis.insert(make_pair(newNum, code++));
        }
        newNum = MOD(MOD(node.x, m), m*k);
        if(MOD(newNum, k)==MOD(n+1, k))
            return make_pair(node.step+1, node.path+"%");
        if(vis.find(newNum)==vis.end()){
            Q.push(Node(newNum, node.step+1, node.path+"%"));
            vis.insert(make_pair(newNum, code++));
        }
    }
    return make_pair(0, string(""));
}

int main()
{
    while(true){
        cin >> n >> k >> m;
        if(!n&&!k&&!m)  return 0;
        pair<int, string> res = bfs();
        printf("%d\n", res.first);
        if(res.first)
            cout << res.second << endl;
    }
    return 0;
}
```

