# 1010 Tempter of the Bone

### **Problem Description**

```
The doggie found a bone in an ancient maze, which fascinated him a lot. However, when he picked it up, the maze began to shake, and the doggie could feel the ground sinking. He realized that the bone was a trap, and he tried desperately to get out of this maze.

The maze was a rectangle with sizes N by M. There was a door in the maze. At the beginning, the door was closed and it would open at the T-th second for a short period of time (less than 1 second). Therefore the doggie had to arrive at the door on exactly the T-th second. In every second, he could move one block to one of the upper, lower, left and right neighboring blocks. Once he entered a block, the ground of this block would start to sink and disappear in the next second. He could not stay at one block for more than one second, nor could he move into a visited block. Can the poor doggie survive? Please help him.
```

### **Input**

```
The input consists of multiple test cases. The first line of each test case contains three integers N, M, and T (1 < N, M < 7; 0 < T < 50), which denote the sizes of the maze and the time at which the door will open, respectively. The next N lines give the maze layout, with each line containing M characters. A character is one of the following:

'X': a block of wall, which the doggie cannot enter;
'S': the start point of the doggie;
'D': the Door; or
'.': an empty block.

The input is terminated with three 0's. This test case is not to be processed.
```

### **Output**

```
For each test case, print in one line "YES" if the doggie can survive, or "NO" otherwise.
```

### **Sample Input**

```
4 4 5
S.X.
..X.
..XD
....
3 4 5
S.X.
..X.
...D
0 0 0
```

### **Sample Output**

```
NO
YES
```

### Notes

```
DFS + 奇偶剪枝

可以把地图看成这样： 
0 1 0 1 0 1 
1 0 1 0 1 0 
0 1 0 1 0 1 
1 0 1 0 1 0 
0 1 0 1 0 1 

不难看出：
从任意 0 走到任意 1 或从任意1到任意0始终是奇数步;
从任意 0 走到任意 0 或从任意1到任意1始终是偶数步;

结论（对于此题）：
所以当遇到从 0 走向 0 但是要求时间是奇数的，或者， 
从 1 走向 0 但是要求时间是偶数的 都可以直接判断不可能到
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

int visited[10][10] = {0};
char maze[10][10];
int n, m, t;

bool dfs(int step, int i, int j){
    if(step==t){
        return maze[i][j] == 'D';
    }
    if(i<1||i>n||j<1||j>m||maze[i][j]=='X')
        return false;
    if(visited[i][j+1]==0){
        visited[i][j+1] = 1;
        if(dfs(step+1, i, j+1))
            return true;
        visited[i][j+1] = 0;
    }
    if(visited[i+1][j]==0){
        visited[i+1][j] = 1;
        if(dfs(step+1, i+1, j))
            return true;
        visited[i+1][j] = 0;
    }
    if(visited[i][j-1]==0){
        visited[i][j-1] = 1;
        if(dfs(step+1, i, j-1))
            return true;
        visited[i][j-1] = 0;
    }
    if(visited[i-1][j]==0){
        visited[i-1][j] = 1;
        if(dfs(step+1, i-1, j))
            return true;
        visited[i-1][j] = 0;
    }
    return false;
}

int main(){
    while(true){
        cin >> n >> m >> t;
        if(!n&&!m&&!t)  return 0;
        memset(visited, 0, sizeof(visited));
        int startI{};
        int startJ{};
        int endI{};
        int endJ{};
        for(int i=1; i<=n; ++i){
            for(int j=1; j<=m; ++j){
                cin >> maze[i][j];
                if(maze[i][j]=='S'){
                    startI = i;
                    startJ = j;
                    visited[i][j] = 1;
                }
                if(maze[i][j]=='D'){
                    endI = i;
                    endJ = j;
                }
            }
        }
        if((t-abs(startI-endI)-abs(startJ-endJ))%2)  // 奇偶剪枝
            cout << "NO" << endl;
        else {
            if(dfs(0, startI, startJ))
                cout << "YES" << endl;
            else
                cout << "NO" << endl;
        }
    }
    return 0;
}
```

