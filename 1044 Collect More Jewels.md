# 1044 Collect More Jewels

### **Problem Description**

```
It is written in the Book of The Lady: After the Creation, the cruel god Moloch 
rebelled against the authority of Marduk the Creator.Moloch stole from Marduk the 
most powerful of all the artifacts of the gods, the Amulet of Yendor, and he hid it 
in the dark cavities of Gehennom, the Under World, where he now lurks, and bides his 
time.

Your goddess The Lady seeks to possess the Amulet, and with it to gain deserved 
ascendance over the other gods.

You, a newly trained Rambler, have been heralded from birth as the instrument of The 
Lady. You are destined to recover the Amulet for your deity, or die in the attempt. 
Your hour of destiny has come. For the sake of us all: Go bravely with The Lady!

If you have ever played the computer game NETHACK, you must be familiar with the 
quotes above. If you have never heard of it, do not worry. You will learn it (and 
love it) soon.

In this problem, you, the adventurer, are in a dangerous dungeon. You are informed 
that the dungeon is going to collapse. You must find the exit stairs within given 
time. However, you do not want to leave the dungeon empty handed. There are lots of 
rare jewels in the dungeon. Try collecting some of them before you leave. Some of the 
jewels are cheaper and some are more expensive. So you will try your best to maximize 
your collection, more importantly, leave the dungeon in time.
```

### **Input**

```
Standard input will contain multiple test cases. The first line of the input is a 
single integer T (1 <= T <= 10) which is the number of test cases. T test cases 
follow, each preceded by a single blank line.

The first line of each test case contains four integers W (1 <= W <= 50), H (1 <= H 
<= 50), L (1 <= L <= 1,000,000) and M (1 <= M <= 10). The dungeon is a rectangle area 
W block wide and H block high. L is the time limit, by which you need to reach the 
exit. You can move to one of the adjacent blocks up, down, left and right in each 
time unit, as long as the target block is inside the dungeon and is not a wall. Time 
starts at 1 when the game begins. M is the number of jewels in the dungeon. Jewels 
will be collected once the adventurer is in that block. This does not cost extra 
time.

The next line contains M integers，which are the values of the jewels.

The next H lines will contain W characters each. They represent the dungeon map in the following notation:
> [*] marks a wall, into which you can not move;
> [.] marks an empty space, into which you can move;
> [@] marks the initial position of the adventurer;
> [<] marks the exit stairs;
> [A] - [J] marks the jewels.
```

### **Output**

```
Results should be directed to standard output. Start each case with "Case #:" on a 
single line, where # is the case number starting from 1. Two consecutive cases should 
be separated by a single blank line. No blank line should be produced after the last 
test case.

If the adventurer can make it to the exit stairs in the time limit, print the sentence 
"The best score is S.", where S is the maximum value of the jewels he can collect 
along the way; otherwise print the word "Impossible" on a single line.
```

### **Sample Input**

```
3

4 4 2 2
100 200
****
*@A*
*B<*
****

4 4 1 2
100 200
****
*@A*
*B<*
****

12 5 13 2
100 200
************
*B.........*
*.********.*
*@...A....<*
************
```

### **Sample Output**

```
Case 1:
The best score is 200.

Case 2:
Impossible

Case 3:
The best score is 300.
```

### Notes

```
bfs求各点之间的最短路径长度，然后dfs剪枝搜索得出最佳方案。（剪枝很重要！！！）
```

### Code

```c++
#include "iostream"
#include "queue"
#include "algorithm"
#include "vector"
#include "cstring"
#include "cstdio"

using namespace std;

struct Node{
    int x;
    int y;
    int step;
    int val;
    explicit Node(int x=0, int y=0, int step=0, int val=0){
        this->x = x;
        this->y = y;
        this->step = step;
        this->val = val;
    }
};

char grid[64][64];
bool visited[12];
int shortestPathLength[12][12];
int W, H, L, M;
Node jewels[12];
int totalValue;
int dx[] = {-1, 1, 0, 0};
int dy[] = {0, 0, -1, 1};


bool legal(const int &x, const int &y){
    return (x>=0&&x<H&&y>=0&&y<W&&grid[x][y]!='*');
}

bool isJewel(const char &c){
    return (c>='A'&&c<='J');
}

int toIndex(const Node &node){
    char c = grid[node.x][node.y];
    if(c=='@')  return 0;
    if(c=='<')  return M+1;
    return c-'A'+1;
}

void bfs(const Node &start){
    queue<Node> Q;
    bool vis[64][64];
    memset(vis, false, sizeof(vis));
    Q.push(start);
    vis[start.x][start.y] = true;
    while(!Q.empty()){
        Node node = Q.front();
        Q.pop();
        if(node.step>L) break;
        if(grid[node.x][node.y]!='.'){
            shortestPathLength[toIndex(start)][toIndex(node)] = node.step;
            shortestPathLength[toIndex(node)][toIndex(start)] = node.step;
        }
        for(int i=0; i<4; ++i){
            int new_x = node.x + dx[i];
            int new_y = node.y + dy[i];
            if(!vis[new_x][new_y]&&legal(new_x, new_y)){
                vis[new_x][new_y] = true;
                Q.push(Node(new_x, new_y, node.step+1));
            }
        }
    }
}



int res = -1;

void dfs(int now, int score, int time){
    if(time+shortestPathLength[now][M+1]>L||res==totalValue)
        return;
    if(now==M+1){
        res = max(res, score);
        return;
    }
    for(int i=0; i<M+2; ++i){
        if(!visited[i]&&shortestPathLength[now][i]){
            visited[i] = true;
            dfs(i, score+jewels[now].val, time+shortestPathLength[now][i]);
            visited[i] = false;
        }
    }
}


int main()
{
    int n;
    int kCase = 0;
    cin >> n;
    int blankLine = false;
    while(n--){
        if(blankLine)   printf("\n");
        if(!blankLine)  blankLine = true;
        cin >> W >> H >> L >> M;
        memset(shortestPathLength, 0, sizeof(shortestPathLength));
        totalValue = 0;
        for(int i=1; i<=M; ++i){
            cin >> jewels[i].val;
            totalValue += jewels[i].val;
        }
        Node start;
        Node exit;
        for(int i=0; i<H; ++i){
            for(int j=0; j<W; ++j){
                cin >> grid[i][j];
                if(grid[i][j]=='@')
                    start = Node(i, j, 0);
                if(grid[i][j]=='<')
                    exit = Node(i, j);
                if(isJewel(grid[i][j])){
                    jewels[grid[i][j]-'A'+1].x = i;
                    jewels[grid[i][j]-'A'+1].y = j;
                }
            }
        }
        jewels[0] = start;
        jewels[M+1] = exit;
        for(int i=0; i<M+2; ++i)    bfs(jewels[i]);
        memset(visited, false, sizeof(visited));
        res = -1;
        dfs(0, 0, 0);
        printf("Case %d:\n", ++kCase);
        if(res==-1)
            printf("Impossible\n");
        else{
            printf("The best score is %d.\n", res);
        }   
    }
    return 0;
}
```

