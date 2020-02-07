# 1177 "Accepted today?"

### **Problem Description**

```
Do you remember a sentence "Accepted today?" Yes, the sentence is mentioned frequently 
in lcy's course "ACM Programming"!
The contest is still in progress this moment. How excited it is! You, smart 
programmer, must have AC some problems today. "Can I get copper medal, silver medal, 
or even golden medal?" Oh, ha-ha! You must be considering this question. And now, the 
last problem of this contest comes.
Give you all submitting data in the contest, and tell you the number of golden medals, silver medals and copper medals; your task is to output someone's contest result.
Easy? Of course! I t is the reason that I designed the problem.
When you have completed this contest, please remember that sentence〃 Accepted today?〃
```

### **Input**

```
Input contains multiple test cases. Each test case starts with five numbers N (4 =< N 
<= 130 -- the total number of attendees), G, S, C (1<=G<=S<=C<N --G, S, C denoting the 
number of golden medals, silver medals and copper medals respectively) and M (0<M<=N). 
The next N lines contain an integer P (1<=P<=8 --number of problems that have been 
solved by someone) and a time T(for example,"02:45:17", meaning 2 hours and 45 minutes 
and 17 seconds consumed according to contest rules) each. You can assume that all 
submit data are different.
A test case starting with 0 0 0 0 0 terminates input and this test case should not to 
be processed.
```

### **Output**

```
For each case, print a sentence in a line, and it must be one of these sentences:
Accepted today? I've got a golden medal :)
Accepted today? I've got a silver medal :)
Accepted today? I've got a copper medal :)
Accepted today? I've got an honor mentioned :)

Note:
You will get an honor mentioned if you can't get copper medal, silver medal or golden 
medal.
```

### **Sample Input**

```
10 1 2 3 6
2 02:45:17
2 02:49:01
2 03:17:58
2 03:21:29
4 07:55:48
3 04:25:42
3 06:57:39
2 02:05:02
2 02:16:45
2 02:41:37
0 0 0 0 0
```

### **Sample Output**

```
Accepted today? I've got a silver medal :)
```

### Notes

```
水题
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


struct Student{
    int solved;
    string time;
};



int main()
{
    while(true){
        int n, g, s, c, m;
        cin >> n >> g >> s >> c >> m;
        if(!n&&!g&&!s&&!c&&!m)  return 0;
        vector<Student> students(n+1);
        for(int i=1; i<=n; ++i){
            cin >> students[i].solved >> students[i].time;
        }
        int pos = 1;
        Student &myself = students[m];
        for(int i=1; i<=n; ++i){
            if(i!=m){
                if(students[i].solved>myself.solved)
                    ++pos;
                else{
                    if(students[i].solved==myself.solved){
                        if(students[i].time<myself.time)
                            ++pos;
                    }
                }
            }
        }
        if(pos<=g)
            printf("Accepted today? I've got a golden medal :)\n");
        else if(pos-g<=s)
            printf("Accepted today? I've got a silver medal :)\n");
        else if(pos-g-s<=c)
            printf("Accepted today? I've got a copper medal :)\n");
        else 
            printf("Accepted today? I've got an honor mentioned :)\n");
    }
    return 0;
}
```

