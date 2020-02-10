# 1058 Humble Numbers

### **Problem Description**

```
A number whose only prime factors are 2,3,5 or 7 is called a humble number. The sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 14, 15, 16, 18, 20, 21, 24, 25, 27, ... shows the first 20 humble numbers.

Write a program to find and print the nth element in this sequence
```

### **Input**

```
The input consists of one or more test cases. Each test case consists of one integer n with 1 <= n <= 5842. Input is terminated by a value of zero (0) for n.
```

### **Output**

```
For each test case, print one line saying "The nth humble number is number.". Depending on the value of n, the correct suffix "st", "nd", "rd", or "th" for the ordinal number nth has to be used like it is shown in the sample output.
```

### **Sample Input**

```
1
2
3
4
11
12
13
21
22
23
100
1000
5842
0
```

### **Sample Output**

```
The 1st humble number is 1.
The 2nd humble number is 2.
The 3rd humble number is 3.
The 4th humble number is 4.
The 11th humble number is 12.
The 12th humble number is 14.
The 13th humble number is 15.
The 21st humble number is 28.
The 22nd humble number is 30.
The 23rd humble number is 32.
The 100th humble number is 450.
The 1000th humble number is 385875.
The 5842nd humble number is 2000000000.
```

### Notes

```
假设丑数已按增序排列,则下一个丑数一定是前面丑数乘以2,3,5,7生成的数中大于当前最大丑数的最小的那个。
```

### Code

```C++
#include "iostream"
#include "cstdio"
#include "set"
#include "vector"
#include "cstdint"

using namespace std;

int64_t factors[] = {2, 3, 5, 7};

int main(){
    vector<int64_t> humbleNumbers;
    humbleNumbers.emplace_back(0);
    set<int64_t, less<>> S;
    S.insert(1);
    while(humbleNumbers.size()<5843){
        int64_t num = *S.begin();
        humbleNumbers.emplace_back(num);
        S.erase(S.begin());
        for(int i=0; i!=4; ++i){
            S.insert(num*factors[i]);
        }
    }
    while(true){
        int n;
        cin >> n;
        if(!n) return 0;
        int64_t res = humbleNumbers[n];
        if((n%100)/10==1){
            printf("The %dth humble number is %lld.\n", n, res);
        }
        else{
            switch(n%10){
                case 1:
                    printf("The %dst humble number is %lld.\n", n, res); break;
                case 2:
                    printf("The %dnd humble number is %lld.\n", n, res); break;
                case 3:
                    printf("The %drd humble number is %lld.\n", n, res); break;
                default:
                    printf("The %dth humble number is %lld.\n", n, res); break;
            }
        }
    }
    return 0;
}
```

