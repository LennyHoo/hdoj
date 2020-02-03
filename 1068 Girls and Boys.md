# 1068 Girls and Boys

### **Problem Description**

```
the second year of the university somebody started a study on the romantic relations between the students. The relation “romantically involved” is defined between one girl and one boy. For the study reasons it is necessary to find out the maximum set satisfying the condition: there are no two students in the set who have been “romantically involved”. The result of the program is the number of students in such a set.

The input contains several data sets in text format. Each data set represents one set of subjects of the study, with the following description:

the number of students
the description of each student, in the following format
student_identifier:(number_of_romantic_relations) student_identifier1 student_identifier2 student_identifier3 ...
or
student_identifier:(0)

The student_identifier is an integer number between 0 and n-1, for n subjects.
For each given data set, the program should write to standard output a line containing the result.
```

### Sample Input

```
7
0: (3) 4 5 6
1: (2) 4 6
2: (0)
3: (0)
4: (2) 0 1
5: (1) 0
6: (2) 0 1
3
0: (2) 1 2
1: (1) 0
2: (1) 0
```

### **Sample Output**

```
5
2
```

### Notes

```
最大独立团 = 顶点数 - 最大匹配数
因为是双向图，所以匈牙利算法求出的是匹配人数，匹配对数是其二分之一。
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;

#define N 505

int n;
bool edge[N][N];
int link[N];
bool visited[N];

bool dfs(int x){
    for(int j=0; j<n; ++j){
        if(!visited[j]&&edge[x][j]){
            visited[j] = true;
            if(link[j]==-1||dfs(link[j])){
                link[j] = x;
                return true;
            }
        }
    }
    return false;
}

int hungary(){
    int res = 0;
    for(int i=0; i<n; ++i){
        memset(visited, false, sizeof(visited));
        if(dfs(i))  ++res;
    }
    return res;
}

int main(){
    while(cin>>n){
        memset(edge, false, sizeof(edge));
        memset(link, -1, sizeof(link));
        for(int k=0; k<n; ++k){
            int i;
            cin >> i;
            getchar(); getchar(); getchar();
            int romanticNum;
            cin >> romanticNum;
            getchar();
            while(romanticNum--){
                int j;
                cin >> j;
                edge[i][j] = true;
            }
        }
        cout << n - hungary()/2 << endl;
    }
    return 0;
}
```

