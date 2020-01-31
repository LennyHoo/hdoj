# 1073 Online Judge

### Online Judge

```
Ignatius is building an Online Judge, now he has worked out all the problems except the Judge System. The system has to read data from correct output file and user's result file, then the system compare the two files. If the two files are absolutly same, then the Judge System return "Accepted", else if the only differences between the two files are spaces(' '), tabs('\t'), or enters('\n'), the Judge System should return "Presentation Error", else the system will return "Wrong Answer".

Given the data of correct output file and the data of user's result file, your task is to determine which result the Judge System will return.
```

### **Input**

```
The input contains several test cases. The first line of the input is a single integer T which is the number of test cases. T test cases follow.
Each test case has two parts, the data of correct output file and the data of the user's result file. Both of them are starts with a single line contains a string "START" and end with a single line contains a string "END", these two strings are not the data. In other words, the data is between the two strings. The data will at most 5000 characters.
```

### **Output**

```
For each test cases, you should output the the result Judge System should return.
```

### **Sample Input**

```
4
START
1 + 2 = 3
END
START
1+2=3
END
START
1 + 2 = 3
END
START
1 + 2 = 3

END
START
1 + 2 = 3
END
START
1 + 2 = 4
END
START
1 + 2 = 3
END
START
1	+	2	=	3
END
```

### **Sample Output**

```
Presentation Error
Presentation Error
Wrong Answer
Presentation Error
```

### Notes

```
C++ STL 
remove() 的返回值是新的 end()
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;



int main(){
    int t;
    cin >> t;
    while(t--){
        string s1;
        string s2;
        string s;
        int n1 = 0;
        int n2 = 0;
        cin >> s;
        getchar();
        while(getline(cin, s)&&s!="END"){
            s1 += s;
            ++n1;
        }
        cin >> s;
        getchar();
        while(getline(cin, s)&&s!="END"){
            s2 += s;
            ++n2;
        }
        if(s1==s2&&n1==n2)
            printf("Accepted\n");
        else{
            s1.erase(remove(s1.begin(), s1.end(), '\n'), s1.end());
            s1.erase(remove(s1.begin(), s1.end(), '\t'), s1.end());
            s1.erase(remove(s1.begin(), s1.end(), ' '), s1.end());
            s2.erase(remove(s2.begin(), s2.end(), '\n'), s2.end());
            s2.erase(remove(s2.begin(), s2.end(), '\t'), s2.end());
            s2.erase(remove(s2.begin(), s2.end(), ' '), s2.end());
            if(s1==s2)
                printf("Presentation Error\n");
            else
                printf("Wrong Answer\n");
        }
    }
    return 0;
}
```

