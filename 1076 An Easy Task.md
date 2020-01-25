# 1076 An Easy Task

### **Problem Description**

```
Ignatius was born in a leap year, so he want to know when he could hold his birthday party. Can you tell him?

Given a positive integers Y which indicate the start year, and a positive integer N, your task is to tell the Nth leap year from year Y.

Note: if year Y is a leap year, then the 1st leap year is year Y.
```

### **Input**

```
The input contains several test cases. The first line of the input is a single integer T which is the number of test cases. T test cases follow.
Each test case contains two positive integers Y and N(1<=N<=10000).
```

### **Output**

```
For each test case, you should output the Nth leap year from year Y.
```

### **Sample Input**

```
3
2005 25
1855 12
2004 10000
```

### **Sample Output**

```
2108
1904
43236
```

### Notes

```
水题
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

bool isLeapYear(int year){
    return (year%4==0&&year%100!=0)||(year%400==0);
}

int main() {
    int n;
    cin >> n;
    while(n--){
        int year{};
        int n{};
        cin >> year >> n;
        while(!isLeapYear(year))    ++year;
        for(int i=2; i<=n; ++i){
            year += 4;
            if(!isLeapYear(year))   --i;
        }
        cout << year << endl;
    }
    return 0;
}
```

