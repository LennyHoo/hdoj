# 1052 Tian Ji -- The Horse Racing

### **Problem Description**

```
Here is a famous story in Chinese history.

"That was about 2300 years ago. General Tian Ji was a high official in the country Qi. He likes to play horse racing with the king and others."

"Both of Tian and the king have three horses in different classes, namely, regular, plus, and super. The rule is to have three rounds in a match; each of the horses must be used in one round. The winner of a single round takes two hundred silver dollars from the loser."

"Being the most powerful man in the country, the king has so nice horses that in each class his horse is better than Tian's. As a result, each time the king takes six hundred silver dollars from Tian."

"Tian Ji was not happy about that, until he met Sun Bin, one of the most famous generals in Chinese history. Using a little trick due to Sun, Tian Ji brought home two hundred silver dollars and such a grace in the next match."

"It was a rather simple trick. Using his regular class horse race against the super class from the king, they will certainly lose that round. But then his plus beat the king's regular, and his super beat the king's plus. What a simple trick. And how do you think of Tian Ji, the high ranked official in China?"

Were Tian Ji lives in nowadays, he will certainly laugh at himself. Even more, were he sitting in the ACM contest right now, he may discover that the horse racing problem can be simply viewed as finding the maximum matching in a bipartite graph. Draw Tian's horses on one side, and the king's horses on the other. Whenever one of Tian's horses can beat one from the king, we draw an edge between them, meaning we wish to establish this pair. Then, the problem of winning as many rounds as possible is just to find the maximum matching in this graph. If there are ties, the problem becomes more complicated, he needs to assign weights 0, 1, or -1 to all the possible edges, and find a maximum weighted perfect matching...

However, the horse racing problem is a very special case of bipartite matching. The graph is decided by the speed of the horses --- a vertex of higher speed always beat a vertex of lower speed. In this case, the weighted bipartite matching algorithm is a too advanced tool to deal with the problem.

In this problem, you are asked to write a program to solve this special case of matching problem.
```

### **Input**

```
The input consists of up to 50 test cases. Each case starts with a positive integer n (n <= 1000) on the first line, which is the number of horses on each side. The next n integers on the second line are the speeds of Tian’s horses. Then the next n integers on the third line are the speeds of the king’s horses. The input ends with a line that has a single 0 after the last test case.
```

### **Output**

```
For each input case, output a line containing a single number, which is the maximum money Tian Ji will get, in silver dollars.
```

### **Sample Input**

```
3
92 83 71
95 87 74
2
20 20
20 20
2
20 19
22 18
0
```

### **Sample Output**

```
200
0
0
```

### Notes

```
首先，将两人的马 降序 排列。 分别用两个头指针两个尾指针，方便进行操作。

（1）如果 田忌 最快的马 比 对手最快的马快，直接比，赢一场，两个头指针加加。

（2）如果 田忌 最快的马 比 对手最快的马慢，那肯定是要输一场的，就拿田忌最慢的马去和对手最快的马比。

（3）如果两人最快的马的速度相同，先不要着急去打平局。此时再看最慢的马。
    <1>如果最慢的马比对手最慢的马快，直接比，赢一场。
    <2>如果最慢的马比对手最慢的马慢，这个最慢的马肯定要输一场，和对手最快的马去比赛。
    这样同样是输，又消耗了对手一个最快的马。
    <3>如果两人最慢的马的速度也相同，，也拿最慢的和对手最快的比较，此时要注意的是
    会不会两人的马的速度都相同。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

bool cmp(int a, int b){
    return a>b;
}

int main(){
    while(true){
        int n;
        cin >> n;
        if(!n)  return 0;
        vector<int> tianji(n);
        vector<int> king(n);
        int win = 0;
        for(int i=0; i<n; ++i)  cin >> tianji[i];
        for(int i=0; i<n; ++i)  cin >> king[i];
        sort(tianji.begin(), tianji.end(), cmp);
        sort(king.begin(), king.end(), cmp);
        int tFast = 0;
        int tLow = tianji.size()-1;
        int kFast = 0;
        int kLow = king.size()-1;
        while(tFast<=tLow&&kFast<=kLow){
            if(tianji[tFast]>king[kFast]){
                ++tFast;
                ++kFast;
                ++win;
            }
            else if(tianji[tFast]<king[kFast]){
                --tLow;
                ++kFast;
                --win;
            }
            else{
            	// 当两者最快的马相等时  
                if(tianji[tLow]>king[kLow]){
                    ++win;
                    --tLow;
                    --kLow;
                }
                else if(tianji[tLow]<king[kLow]){
                    --win;
                    --tLow;
                    ++kFast;
                }
                else{
                    if(tianji[tLow]<king[kFast])
                        --win;
                    --tLow;
                    ++kFast;
                }
            }
        }
        cout << win*200 << endl;
    }
    return 0;
}
```

