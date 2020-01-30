# 1083 Courses

### **Problem Description**

```
Consider a group of N students and P courses. Each student visits zero, one or more than one courses. Your task is to determine whether it is possible to form a committee of exactly P students that satisfies simultaneously the conditions:

. every student in the committee represents a different course (a student can represent a course if he/she visits that course)

. each course has a representative in the committee

Your program should read sets of data from a text file. The first line of the input file contains the number of the data sets. Each data set is presented in the following format:

P N
Count1 Student1 1 Student1 2 ... Student1 Count1
Count2 Student2 1 Student2 2 ... Student2 Count2
......
CountP StudentP 1 StudentP 2 ... StudentP CountP

The first line in each data set contains two positive integers separated by one blank: P (1 <= P <= 100) - the number of courses and N (1 <= N <= 300) - the number of students. The next P lines describe in sequence of the courses . from course 1 to course P, each line describing a course. The description of course i is a line that starts with an integer Count i (0 <= Count i <= N) representing the number of students visiting course i. Next, after a blank, you'll find the Count i students, visiting the course, each two consecutive separated by one blank. Students are numbered with the positive integers from 1 to N.

There are no blank lines between consecutive sets of data. Input data are correct.

The result of the program is on the standard output. For each input data set the program prints on a single line "YES" if it is possible to form a committee and "NO" otherwise. There should not be any leading blanks at the start of the line.

An example of program input and output:
```

### **Sample Input**

```
2
3 3
3 1 2 3
2 1 2
1 1
3 3
2 1 3
2 1 3
1 1
```

### **Sample Output**

```
YES
NO 
```

### Notes

```
匈牙利算法：https://www.cnblogs.com/memory2018/p/10563861.html
匈牙利算法的思想非常暴力，就是对于个边，能连就直接连，不能连就尝试让之前的点给当前点腾出来一个点。
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

int edge[500][500];
bool visited[500] = {false};
int link[500];
int p, n;

bool dfs(int i){
    for(int j=1; j<=n; ++j){
        if(!visited[j]&&edge[i][j]){
            visited[j] = true;
            if(link[j]==-1||dfs(link[j])){
                link[j] = i;
                return true;
            }
        }
    }
    return false;
}

int Hungary(){
    int res = 0;
    memset(link, -1, sizeof(link));
    for(int i=1; i<=p; ++i){
        memset(visited, false, sizeof(visited));
        if(dfs(i))  ++res;
    }
    return res;
}

int main(){
    ios::sync_with_stdio(false);
    int t;
    cin >> t;
    while(t--){
        cin >> p >> n;
        memset(edge, 0, sizeof(edge));
        for(int i=1; i<=p; ++i){
            int count;
            cin >> count;
            for(int c=1; c<=count; ++c){
                int j;
                cin >> j;
                edge[i][j] = 1;
            }
        }
        if(Hungary()==p)
            printf("YES\n");
        else
            printf("NO\n");
    }
    return 0;
}
```

