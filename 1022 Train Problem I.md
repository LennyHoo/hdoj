# 1022 Train Problem I

### **Problem Description**

```
As the new term comes, the Ignatius Train Station is very busy nowadays. A lot of student want to get back to school by train(because the trains in the Ignatius Train Station is the fastest all over the world ^v^). But here comes a problem, there is only one railway where all the trains stop. So all the trains come in from one side and get out from the other side. For this problem, if train A gets into the railway first, and then train B gets into the railway before train A leaves, train A can't leave until train B leaves. The pictures below figure out the problem. Now the problem for you is, there are at most 9 trains in the station, all the trains has an ID(numbered from 1 to n), the trains get into the railway in an order O1, your task is to determine whether the trains can get out in an order O2.
```

### Input

```
The input contains several test cases. Each test case consists of an integer, the number of trains, and two strings, the order of the trains come in:O1, and the order of the trains leave:O2. The input is terminated by the end of file. More details in the Sample Input.
```

### **Output**

```
The output contains a string "No." if you can't exchange O2 to O1, or you should output a line contains "Yes.", and then output your way in exchanging the order(you should output "in" for a train getting into the railway, and "out" for a train getting out of the railway). Print a line contains "FINISH" after each test case. More details in the Sample Output.
```

### **Sample Input**

```
3 123 321
3 123 312
```

### **Sample Output**

```
Yes.
in
in
in
out
out
out
FINISH
No.
FINISH
```

### Notes

```
模拟法：用栈模拟火车的进站和出站过程，每当一个火车进站就将栈的顶部元素与出站顺序o2进行比对，判断是否立即出站(注意：这里使用的是while)。用一个列表储存这些进站和出站操作。
```

### Code

```
#include "iostream"
#include "cstdio"
#include "cstring"
#include "vector"
#include "stack"

using namespace std;


int main() {
    int n;
    while(cin>>n){
        string o1;
        string o2;
        cin >> o1 >> o2;
        int o2Pointer = 0;
        vector<string> process;
        stack<char> station;
        for(int i=0; i<o1.length(); ++i){
            station.push(o1[i]);
            process.emplace_back("in");
            while(!station.empty()&&station.top()==o2[o2Pointer]){
                station.pop();
                process.emplace_back("out");
                ++o2Pointer;
            }
        }
        for(int i=o2Pointer; i<o2.length(); ++i){
            if(station.top()!=o2[i]){
                printf("No.\n");
                printf("FINISH\n");
                break;
            }
            else{
                station.pop();
                process.emplace_back("out");
            }
        }
        if(station.empty()){
            cout << "Yes." << endl;
            for(auto it=process.begin(); it!=process.end(); ++it){
                cout << *it << endl;
            }
            printf("FINISH\n");
        }
    }
    return 0;
}
```

