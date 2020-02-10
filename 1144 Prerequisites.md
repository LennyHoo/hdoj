# 1144 Prerequisites?

### **Problem Description**

```
Freddie the frosh has chosen to take k courses. To meet the degree requirements, he 
must take courses from each of several categories. Can you assure Freddie that he will 
graduate, based on his course selection?
```

### **Input**

```
Input consists of several test cases. For each case, the first line of input contains 
1 ≤ k ≤ 100, the number of courses Freddie has chosen, and 0 ≤ m ≤ 100, the number of 
categories. One or more lines follow containing k 4-digit integers follow; each is the 
number of a course selected by Freddie. Each category is represented by a line 
containing 1 ≤ c ≤ 100, the number of courses in the category, 0 ≤ r ≤ c, the minimum 
number of courses from the category that must be taken, and the c course numbers in 
the category. Each course number is a 4-digit integer. The same course may fulfil 
several category requirements. Freddie's selections, and the course numbers in any 
particular category, are distinct. A line containing 0 follows the last test case.
```

### **Output**

```
For each test case, output a line containing "yes" if Freddie's course selection meets 
the degree requirements; otherwise output "no."
```

### **Sample Input**

```
3 2
0123 9876 2222
2 1 8888 2222
3 2 9876 2222 7654 
3 2
0123 9876 2222
2 2 8888 2222
3 2 7654 9876 2222
0
```

### **Sample Output**

```
yes
no
```

### Notes

```
水题
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;


int main(){
    while(true){
        int k;
        cin >> k;
        if(!k)  return 0;
        int m;
        cin >> m;
        vector<int> chosedCourse(k);
        for(int i=0; i<k; ++i)
            cin >> chosedCourse[i];
        bool ok = true;
        while(m--){
            int c, r;
            cin >> c >> r;
            int chosedNum = 0;
            while(c--){
                int course;
                cin >> course;
                auto it = find(chosedCourse.begin(), chosedCourse.end(), course);
                if(it!=chosedCourse.end())
                    ++chosedNum;
            }
            if(chosedNum<r){
                ok = false;
            }
        }
        if(ok)
            cout << "yes" << endl;
        else
            cout << "no" << endl;
    }
    return 0;
}
```

