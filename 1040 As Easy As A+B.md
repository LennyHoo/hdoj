# 1040 As Easy As A+B

### **Problem Description**

```
These days, I am thinking about a question, how can I get a problem as easy as A+B? It is fairly difficulty to do such a thing. Of course, I got it after many waking nights.
Give you some integers, your task is to sort these number ascending (升序).
You should know how easy the problem is now!
Good luck!
```

### **Input**

```
Input contains multiple test cases. The first line of the input is a single integer T which is the number of test cases. T test cases follow. Each test case contains an integer N (1<=N<=1000 the number of integers to be sorted) and then N integers follow in the same line.
It is guarantied that all integers are in the range of 32-int.
```

### **Output**

```
For each case, print the sorting result, and one line one case.
```

### **Sample Input**

```
2
3 2 1 3
9 1 4 7 2 5 8 3 6 9
```

### **Sample Output**

```
1 2 3
1 2 3 4 5 6 7 8 9
```

### Notes

```
题如其名，看了 Discuss ，这题用冒泡排序都可以AC...
```

### Code

```c++
#include "iostream"
#include "cstdio"
#include "cstring"
#include "vector"
#include "algorithm"

using namespace std;


int main() {
    int t{};
    cin >> t;
    while(t--){
        int n{};
        cin >> n;
        vector<int> nums;
        while(n--){
            int num;
            cin >> num;
            nums.push_back(num);
        }
        sort(nums.begin(), nums.end());
        for(int i=0; i<nums.size()-1; ++i)
            printf("%d ", nums[i]);
        printf("%d\n", nums[nums.size()-1]);
    }
    return 0;
}
```

