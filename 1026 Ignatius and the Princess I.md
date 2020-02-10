# 1026 Ignatius and the Princess I

### **Problem Description**

```
The Princess has been abducted by the BEelzebub feng5166, our hero Ignatius has to rescue our pretty Princess. Now he gets into feng5166's castle. The castle is a large labyrinth. To make the problem simply, we assume the labyrinth is a N*M two-dimensional array which left-top corner is (0,0) and right-bottom corner is (N-1,M-1). Ignatius enters at (0,0), and the door to feng5166's room is at (N-1,M-1), that is our target. There are some monsters in the castle, if Ignatius meet them, he has to kill them. Here is some rules:

1.Ignatius can only move in four directions(up, down, left, right), one step per second. A step is defined as follow: if current position is (x,y), after a step, Ignatius can only stand on (x-1,y), (x+1,y), (x,y-1) or (x,y+1).
2.The array is marked with some characters and numbers. We define them like this:
. : The place where Ignatius can walk on.
X : The place is a trap, Ignatius should not walk on it.
n : Here is a monster with n HP(1<=n<=9), if Ignatius walk on it, it takes him n seconds to kill the monster.

Your task is to give out the path which costs minimum seconds for Ignatius to reach target position. You may assume that the start position and the target position will never be a trap, and there will never be a monster at the start position.
```

### **Input**

```
The input contains several test cases. Each test case starts with a line contains two numbers N and M(2<=N<=100,2<=M<=100) which indicate the size of the labyrinth. Then a N*M two-dimensional array follows, which describe the whole labyrinth. The input is terminated by the end of file. More details in the Sample Input
```

### **Output**

```
For each test case, you should output "God please help our poor hero." if Ignatius can't reach the target position, or you should output "It takes n seconds to reach the target position, let me show you the way."(n is the minimum seconds), and tell our hero the whole path. Output a line contains "FINISH" after each test case. If there are more than one path, any one is OK in this problem. More details in the Sample Output.
```

### **Sample Input**

```
5 6
.XX.1.
..X.2.
2...X.
...XX.
XXXXX.
5 6
.XX.1.
..X.2.
2...X.
...XX.
XXXXX1
5 6
.XX...
..XX1.
2...X.
...XX.
XXXXX.
```

### **Sample Output**

```
It takes 13 seconds to reach the target position, let me show you the way.
1s:(0,0)->(1,0)
2s:(1,0)->(1,1)
3s:(1,1)->(2,1)
4s:(2,1)->(2,2)
5s:(2,2)->(2,3)
6s:(2,3)->(1,3)
7s:(1,3)->(1,4)
8s:FIGHT AT (1,4)
9s:FIGHT AT (1,4)
10s:(1,4)->(1,5)
11s:(1,5)->(2,5)
12s:(2,5)->(3,5)
13s:(3,5)->(4,5)
FINISH
It takes 14 seconds to reach the target position, let me show you the way.
1s:(0,0)->(1,0)
2s:(1,0)->(1,1)
3s:(1,1)->(2,1)
4s:(2,1)->(2,2)
5s:(2,2)->(2,3)
6s:(2,3)->(1,3)
7s:(1,3)->(1,4)
8s:FIGHT AT (1,4)
9s:FIGHT AT (1,4)
10s:(1,4)->(1,5)
11s:(1,5)->(2,5)
12s:(2,5)->(3,5)
13s:(3,5)->(4,5)
14s:FIGHT AT (4,5)
FINISH
God please help our poor hero.
FINISH
```

### Notes

```
bfs + priority_queue
```

### Code

```C++
#include "iostream"
#include "cstdio"
#include "vector"
#include "queue"
#include "cstring"
#include "cctype"

using namespace std;


class Node{
public:
    int x;
    int y;
    int type;
    int time;
    Node *preNode;
public:
    Node(){}
    Node(int x, int y, int time, int type, Node* preNode=nullptr){
        this->x = x;
        this->y = y;
        this->time = time;
        this->type = type;
        this->preNode = preNode;
    }
    ~Node()= default;
    bool operator<(const Node &node) const{
        return node.time<time;
    }
};


int n, m;
char grid[105][105];
bool visited[105][105];
vector<Node*> bestPath;
Node *lastNode;
int dx[] = { -1, 1, 0, 0 }, dy[] = { 0, 0, 1, -1 };

bool legal(int x, int y){
    return (x>=0&&x<n&&y>=0&&y<m&&grid[x][y]!='X');
}

struct cmp{
    bool operator()(Node* a, Node* b){
        return (a->time>b->time);
    }
};

Node* subBfs(priority_queue<Node*, vector<Node*>, cmp> &Q, Node *preNode, int x, int y){
    Node *nextNode = nullptr;
    if(legal(x, y)&&!visited[x][y]){
        if(isdigit(grid[x][y]))
            nextNode = new Node(x, y, preNode->time+1+(grid[x][y]-'0'), 1, preNode);
        else
            nextNode = new Node(x, y, preNode->time+1, 0, preNode);
        Q.push(nextNode);
        visited[x][y] = true;
    }
    return nextNode;
}

Node* bfs(){
    priority_queue<Node*, vector<Node*>, cmp> Q;
    Node *start = new Node(0, 0, 0, 0);
    visited[0][0] = true;
    Q.push(start);
    while(!Q.empty()){
        Node *node = Q.top();
        Q.pop();
        for(int i=0; i<4; ++i){
            Node *nextNode = subBfs(Q, node, node->x+dx[i], node->y+dy[i]);
            if(nextNode!=nullptr){
                if(nextNode->x==n-1&&nextNode->y==m-1){
                    return nextNode;
                }
            }
        }
    }
    return nullptr;
}

int main(){
    while(cin>>n>>m){
        for(int i=0; i<n; ++i){
            for(int j=0; j<m; ++j)
                cin >> grid[i][j];
        }
        bestPath.clear();
        memset(visited, false, sizeof(visited));
        lastNode = bfs();
        bestPath.clear();
        Node *p = lastNode;
        while(p!=nullptr){
            bestPath.insert(bestPath.begin(), p);
            p = p->preNode;
        }
        if(lastNode==nullptr){
            printf("God please help our poor hero.\n");
        }
        else{
            printf("It takes %d seconds to reach the target position, 
                   let me show you the way.\n", lastNode->time);
            Node start = *bestPath[0];
            for(size_t i=1; i<bestPath.size(); ++i){
                Node pre = *bestPath[i-1];
                Node now = *bestPath[i];
                if(now.type==0){
                    printf("%ds:(%d,%d)->(%d,%d)\n", 
                           now.time, pre.x, pre.y, now.x, now.y);
                }
                else{
                    int hp = grid[now.x][now.y]-'0';
                    printf("%ds:(%d,%d)->(%d,%d)\n",
                            now.time-hp, pre.x, pre.y, now.x, now.y);
                    for(int j=hp-1; j>=0; --j){
                        printf("%ds:FIGHT AT (%d,%d)\n", now.time-j, now.x, now.y);
                    }
                }
            }
        }
        printf("FINISH\n");
    }
    return 0;
}
```

