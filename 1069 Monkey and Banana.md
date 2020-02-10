# 1069 Monkey and Banana

### **Problem Description**

```
A group of researchers are designing an experiment to test the IQ of a monkey. They will hang a banana at the roof of a building, and at the mean time, provide the monkey with some blocks. If the monkey is clever enough, it shall be able to reach the banana by placing one block on the top another to build a tower and climb up to get its favorite food.

The researchers have n types of blocks, and an unlimited supply of blocks of each type. Each type-i block was a rectangular solid with linear dimensions (xi, yi, zi). A block could be reoriented so that any two of its three dimensions determined the dimensions of the base and the other dimension was the height.

They want to make sure that the tallest tower possible by stacking blocks can reach the roof. The problem is that, in building a tower, one block could only be placed on top of another block as long as the two base dimensions of the upper block were both strictly smaller than the corresponding base dimensions of the lower block because there has to be some space for the monkey to step on. This meant, for example, that blocks oriented to have equal-sized bases couldn't be stacked.

Your job is to write a program that determines the height of the tallest tower the monkey can build with a given set of blocks.
```

### **Input**

```
The input file will contain one or more test cases. The first line of each test case contains an integer n,
representing the number of different blocks in the following data set. The maximum value for n is 30.
Each of the next n lines contains three integers representing the values xi, yi and zi.
Input is terminated by a value of zero (0) for n.
```

### **Output**

```
For each test case, print one line containing the case number (they are numbered sequentially starting from 1) and the height of the tallest possible tower in the format "Case case: maximum height = height".
```

### **Sample Input**

```
1
10 20 30
2
6 8 10
5 5 5
7
1 1 1
2 2 2
3 3 3
4 4 4
5 5 5
6 6 6
7 7 7
5
31 41 59
26 53 58
97 93 23
84 62 64
33 83 27
0
```

### **Sample Output**

```
Case 1: maximum height = 40
Case 2: maximum height = 21
Case 3: maximum height = 28
Case 4: maximum height = 342
```

### Notes

```
状态转移：

dp[x]表示用上第x块木块时能搭的最高高度。

dp[i] = max(dp[i],dp[j]+data[i].h); j ∈[1,i-1];

边界条件（初始化）:dp[i] = data[i].h （因为每个方块最优解至少比他自身的高度要高）

记得在状态转移前要加上条件（if(data[j].x > data[i].x && data[j].y > data[i].y)）
因为虽然进行排序了，还是存在长度相等的情况，所以要排除，另外宽度本身就是无序状态的。所以更要判断。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

class Block{
public:
    int length{};
    int width{};
    int height{};
public:
    Block(){

    }
    Block(int x, int y, int z){
        this->length = x;
        this->width = y;
        this->height = z;
    }
    bool operator<(const Block &block){
        return this->length>block.length;
    }
};


Block blocks[100];
int n;

int main(){
    int kCase = 0;
    while(true){
        cin >> n;
        if(!n)  return 0;
        for(int i=0; i<n; ++i){
            int x, y, z;
            cin >> x >> y >> z;
            blocks[3*i+1] = Block(max(x,y), min(x,y), z);
            blocks[3*i+2] = Block(max(x,z), min(x,z), y);
            blocks[3*i+3] = Block(max(y,z), min(y,z), x);
        }
        sort(blocks+1, blocks+3*n+1);
        int dp[100];
        dp[1] = blocks[1].height;
        int ans = 0;
        for(int i=2; i<=3*n; ++i){
            dp[i] = blocks[i].height;
            for(int j=i-1; j>=1; --j){
               if(blocks[j].length>blocks[i].length&&blocks[j].width>blocks[i].width)
                    dp[i] = max(dp[i], dp[j]+blocks[i].height);
            }
            ans = max(ans, dp[i]);
        }
        printf("Case %d: maximum height = %d\n", ++kCase, ans);
    }
    return 0;
}
```

