# 1072 Nightmare

### **Problem Description**

```
Ignatius had a nightmare last night. He found himself in a labyrinth with a time bomb on him. The labyrinth has an exit, Ignatius should get out of the labyrinth before the bomb explodes. The initial exploding time of the bomb is set to 6 minutes. To prevent the bomb from exploding by shake, Ignatius had to move slowly, that is to move from one area to the nearest area(that is, if Ignatius stands on (x,y) now, he could only on (x+1,y), (x-1,y), (x,y+1), or (x,y-1) in the next minute) takes him 1 minute. Some area in the labyrinth contains a Bomb-Reset-Equipment. They could reset the exploding time to 6 minutes.

Given the layout of the labyrinth and Ignatius' start position, please tell Ignatius whether he could get out of the labyrinth, if he could, output the minimum time that he has to use to find the exit of the labyrinth, else output -1.

Here are some rules:
1. We can assume the labyrinth is a 2 array.
2. Each minute, Ignatius could only get to one of the nearest area, and he should not walk out of the border, of course he could not walk on a wall, too.
3. If Ignatius get to the exit when the exploding time turns to 0, he can't get out of the labyrinth.
4. If Ignatius get to the area which contains Bomb-Rest-Equipment when the exploding time turns to 0, he can't use the equipment to reset the bomb.
5. A Bomb-Reset-Equipment can be used as many times as you wish, if it is needed, Ignatius can get to any areas in the labyrinth as many times as you wish.
6. The time to reset the exploding time can be ignore, in other words, if Ignatius get to an area which contain Bomb-Rest-Equipment, and the exploding time is larger than 0, the exploding time would be reset to 6.
```

### **Input**

```
The input contains several test cases. The first line of the input is a single integer T which is the number of test cases. T test cases follow.
Each test case starts with two integers N and M(1<=N,Mm=8) which indicate the size of the labyrinth. Then N lines follow, each line contains M integers. The array indicates the layout of the labyrinth.
There are five integers which indicate the different type of area in the labyrinth:
0: The area is a wall, Ignatius should not walk on it.
1: The area contains nothing, Ignatius can walk on it.
2: Ignatius' start position, Ignatius starts his escape from this position.
3: The exit of the labyrinth, Ignatius' target position.
4: The area contains a Bomb-Reset-Equipment, Ignatius can delay the exploding time by walking to these areas.
```

### **Output**

```
For each test case, if Ignatius can get out of the labyrinth, you should output the minimum time he needs, else you should just output -1.
```

### **Sample Input**

```
3
3 3
2 1 1
1 1 0
1 1 3
4 8
2 1 1 0 1 1 1 0
1 0 4 1 1 0 4 1
1 0 0 0 0 0 0 1
1 1 1 4 1 1 1 3
5 8
1 2 1 1 1 1 1 4 
1 0 0 0 1 0 0 1 
1 4 1 0 1 1 0 1 
1 0 0 0 0 3 0 1 
1 1 4 1 1 1 1 1 
```

### **Sample Output**

```
4
-1
13
```

### Notes

```
bfs + priority_queue
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;

int grid[10][10];
int n, m;
int startX, startY;
int dx[] = {1, -1, 0, 0};
int dy[] = {0, 0, 1, -1};

struct Node{
    int step{};
    int x;
    int y;
    int resetTime{};
    explicit Node(){}
    explicit Node(int step, int x, int y, int resetTime){
        this->step = step;
        this->x = x;
        this->y = y;
        this->resetTime = resetTime;
    }
};

struct cmp{
    bool operator()(Node a, Node b){
        return (a.step+a.resetTime>b.step+b.resetTime);
    }
};

bool legal(int x, int y){
    return (x>=1&&x<=n&&y>=1&&y<=m&&grid[x][y]!=0);
}

int bfs(){
    priority_queue<Node, vector<Node>, cmp> Q;
    Q.push(Node(0, startX, startY, 0));
    while(!Q.empty()){
        Node node = Q.top();
        Q.pop();
        if(node.step>=5) continue;
        for(int i=0; i<4; ++i){
            int newX = node.x+dx[i];
            int newY = node.y+dy[i];
            if(legal(newX, newY)&&grid[newX][newY]!=-1){
                if(grid[newX][newY]==4){
                    Q.push(Node(0, newX, newY, node.step+node.resetTime+1));
                    grid[newX][newY] = -1;
                }
                else{
                    if(grid[newX][newY]==3)
                        return (node.step+1+node.resetTime);
                    Q.push(Node(node.step+1, newX, newY, node.resetTime));
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
        cin >> n >> m;
        for(int i=1; i<=n; ++i){
            for(int j=1; j<=m; ++j){
                cin >> grid[i][j];
                if(grid[i][j]==2){
                    startX = i;
                    startY = j;
                }
            }
        }
        cout << bfs() << endl;
    }
    return 0;
}
```

