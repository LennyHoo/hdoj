# 1084 What Is Your Grade?

### **Problem Description**

```
“Point, point, life of student!”
This is a ballad（歌谣）well known in colleges, and you must care about your score in this exam too. How many points can you get? Now, I told you the rules which are used in this course.
There are 5 problems in this final exam. And I will give you 100 points if you can solve all 5 problems; of course, it is fairly difficulty for many of you. If you can solve 4 problems, you can also get a high score 95 or 90 (you can get the former(前者) only when your rank is in the first half of all students who solve 4 problems). Analogically（以此类推）, you can get 85、80、75、70、65、60. But you will not pass this exam if you solve nothing problem, and I will mark your score with 50.
Note, only 1 student will get the score 95 when 3 students have solved 4 problems.
I wish you all can pass the exam!
Come on!
```

### **Input**

```
Input contains multiple test cases. Each test case contains an integer N (1<=N<=100, the number of students) in a line first, and then N lines follow. Each line contains P (0<=P<=5 number of problems that have been solved) and T（consumed time）. You can assume that all data are different when 0<p.
A test case starting with a negative integer terminates the input and this test case should not to be processed.
```

### **Output**

```
Output the scores of N students in N lines for each case, and there is a blank line after each case.
```

### **Sample Input**

```
4
5 06:30:17
4 07:31:27
4 08:12:12
4 05:23:13
1
5 06:30:17
-1
```

### **Sample Output**

```
100
90
90
95

100
```

### Notes

```
"Note, only 1 student will get the score 95 when 3 students have solved 4 problems.""
忽略这句话，就ac了
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

class Student{
public:
    int solved;
    string time;
    int score;
    int index;
};

bool cmp(const Student &a, const Student &b){
    if(a.solved==b.solved)
        return a.time<b.time;
    else
        return a.solved>b.solved;
}

bool cmpIndex(const Student &a, const Student &b){
    return (a.index<b.index);
}

int times[] = {0, 0, 0, 0, 0, 0};
int scores[] = {50, 60, 70, 80, 90, 100};
int counts[] = {0, 0, 0, 0, 0, 0};
int start[6] = {-1};
int halfRank[] = {0, 0, 0, 0, 0, 0};

int main(){
    while(true){
        int n;
        cin >> n;
        if(n==-1)   return 0;
        vector<Student> students(n+1);
        memset(times, 0, sizeof(times));
        memset(counts, 0, sizeof(counts));
        memset(start, -1, sizeof(start));
        for(int i=1; i<=n; ++i){
            cin >> students[i].solved;
            cin >> students[i].time;
            students[i].index = i;
        }
        sort(students.begin()+1, students.end(), cmp);
        for(int i=0; i<=5; ++i){
            for(size_t j=1; j<=n; ++j){
                if(students[j].solved==i&&start[i]==-1){
                    start[i] = j;
                }
                if(students[j].solved==i)
                    ++counts[i];
            }
        }
        for(int i=0; i<=5; ++i){
            halfRank[i] = start[i] + counts[i]/2;
        }
        for(int i=1; i<=n; ++i){
            if(students[i].solved==5){
                students[i].score = 100;
            }
            else if(students[i].solved==0){
                students[i].score = 50;
            }
            else{
                if(i<halfRank[students[i].solved]){
                    students[i].score = scores[students[i].solved] + 5;
                }
                else{
                    students[i].score = scores[students[i].solved];
                }
            }
            ++times[students[i].solved];
        }
        sort(students.begin()+1, students.end(), cmpIndex);
        for(int i=1; i<=n; ++i){
            cout << students[i].score << endl;
        }
        cout << endl;
    }
    return 0;
}
```



