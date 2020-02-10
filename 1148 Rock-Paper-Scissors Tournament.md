# 1148 Rock-Paper-Scissors Tournament

### **Problem Description**

```
Rock-Paper-Scissors is game for two players, A and B, who each choose, independently 
of the other, one of rock, paper, or scissors. A player chosing paper wins over a 
player chosing rock; a player chosing scissors wins over a player chosing paper; a 
player chosing rock wins over a player chosing scissors. A player chosing the same 
thing as the other player neither wins nor loses.
A tournament has been organized in which each of n players plays k rock-scissors-paper 
games with each of the other players - k games in total. Your job is to compute the 
win average for each player, defined as w / (w + l) where w is the number of games 
won, and l is the number of games lost, by the player.
```

### Input

```
Input consists of several test cases. The first line of input for each case contains 1 
≤ n ≤ 100 1 ≤ k ≤ 100 as defined above. For each game, a line follows containing p1, 
m1, p2, m2. 1 ≤ p1 ≤ n and 1 ≤ p2 ≤ n are distinct integers identifying two players; 
m1 and m2 are their respective moves ("rock", "scissors", or "paper"). A line 
containing 0 follows the last test case.
```

### **Output**

```
Output one line each for player 1, player 2, and so on, through player n, giving the 
player's win average rounded to three decimal places. If the win average is undefined, 
output "-". Output an empty line between cases.
```

### **Sample Input**

```
2 4
1 rock 2 paper
1 scissors 2 paper
1 rock 2 rock
2 rock 1 scissors
2 1
1 rock 2 paper
0
```

### **Sample Output**

```
0.333
0.667

0.000
1.000
```

### Notes

```
最后一个 case 末尾不要加空行
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


struct Player{
    int win = 0;
    int lost = 0;
};

int compare(const string &a, const string &b){
    if(a==b)    return 0;
    else if((a=="rock"&&b=="scissors")
                ||(a=="scissors"&&b=="paper")
                    ||(a=="paper"&&b=="rock"))
        return 1;
    else 
        return -1;
}

int main()
{
    bool flag = true;
    while(true){
        int n;
        cin >> n;
        if(!n)  return 0;
        if(!flag)   printf("\n");
        if(flag)    flag = false;
        vector<Player> players(n+1);
        int k;
        cin >> k;
        for(int i=0; i<k; ++i){
            int p1, p2;
            string m1, m2;
            cin >> p1 >> m1 >> p2 >> m2;
            int res = compare(m1, m2);
            if(res==1){
                ++players[p1].win;
                ++players[p2].lost;
            }
            if(res==-1){
                ++players[p1].lost;
                ++players[p2].win;
            }
        }
        for(int i=1; i<=n; ++i){
            if(!players[i].win&&!players[i].lost)
                printf("-\n");
            else 
                printf("%.3lf\n", 
                    players[i].win*1.f/(players[i].win+players[i].lost));
        }
    }
    return 0;
}
```

