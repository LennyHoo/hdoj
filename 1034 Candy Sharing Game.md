# 1034 Candy Sharing Game

### **Problem Description**

```
A number of students sit in a circle facing their teacher in the center. Each student initially has an even number of pieces of candy. When the teacher blows a whistle, each student simultaneously gives half of his or her candy to the neighbor on the right. Any student, who ends up with an odd number of pieces of candy, is given another piece by the teacher. The game ends when all students have the same number of pieces of candy.
Write a program which determines the number of times the teacher blows the whistle and the final number of pieces of candy for each student from the amount of candy each child starts with.
```

### **Input**

```
The input may describe more than one game. For each game, the input begins with the number N of students, followed by N (even) candy counts for the children counter-clockwise around the circle. The input ends with a student count of 0. Each input number is on a line by itself.
```

### **Output**

```
For each game, output the number of rounds of the game followed by the amount of candy each child ends up with, both on one line.
```

### **Sample Input**

```
6
36
2
2
2
2
2
11
22
20
18
16
14
12
10
8
6
4
2
4
2
4
6
8
0
```

### **Sample Output**

```
15 14
17 22
4 8
```

### Notes

```
水题，暴力模拟法。
```

### Code

```C++
#include "iostream"
#include "cstdio"
#include "cstring"
#include "vector"
#include "stack"
#include "algorithm"
#include "string"
#include "cstdint"

using namespace std;

bool isEqual(const int nums[], int length){
    int target = nums[0];
    for(int i=1; i<length; ++i){
        if(nums[i]!=target)
            return false;
    }
    return true;
}

int main() {
    while(true){
        int n;
        cin >> n;
        if(!n)  return 0;
        int *children = new int[n];
        for(int i=0; i<n; ++i)
            cin >> children[i];
        int times = 0;
        while(!isEqual(children, n)){
            ++times;
            for(int i=0; i<n; ++i)
                children[i] /= 2;
            int lastOne = children[n-1];
            for(int i=n-2; i>=0; --i)
                children[i+1] += children[i];
            children[0] += lastOne;
            for(int i=0; i<n; ++i){
                if(children[i]%2)
                    ++children[i];
            }
        }
        cout << times << " " << children[0] << endl;
        delete[] children;
    }
    return 0;
}
```

