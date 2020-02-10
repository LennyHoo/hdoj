# 1036 Average is not Fast Enough!

### **Problem Description**

```
A relay is a race for two or more teams of runners. Each member of a team runs one section of the race. Your task is to help to evaluate the results of a relay race.

You have to process several teams. For each team you are given a list with the running times for every section of the race. You are to compute the average time per kilometer over the whole distance. That's easy, isn't it?
So if you like the fun and challenge competing at this contest, perhaps you like a relay race, too. Students from Ulm participated e.g. at the "SOLA" relay in Zurich, Switzerland. For more information visit http://www.sola.asvz.ethz.ch/ after the contest is over.
```

### **Input**

```
The first line of the input specifies the number of sections n followed by the total distance of the relay d in kilometers. You may safely assume that 1 <= n <= 20 and 0.0 < d < 200.0. Every following line gives information about one team: the team number t (an integer, right-justified in a field of width 3) is followed by the n results for each section, separated by a single space. These running times are given in the format "h:mm:ss" with integer numbers for the hours, minutes and seconds, respectively. In the special case of a runner being disqualified, the running time will be denoted by "-:--:--". Finally, the data on every line is terminated by a newline character. Input is terminated by EOF.
```

### **Output**

```
For each team output exactly one line giving the team's number t right aligned in a field of width 3, and the average time for this team rounded to whole seconds in the format "m:ss". If at least one of the team's runners has been disqualified, output "-" instead. Adhere to the sample output for the exact format of presentation.
```

### **Sample Input**

```
2 12.5
  5 0:23:21 0:25:01
 42 0:23:32 -:--:--
  7 0:33:20 0:41:35
```

### **Sample Output**

```
 5: 3:52 min/km
 42: -
  7: 6:00 min/km
```

### Nodes

```
遇到 '-' 不要 break，因为后面还在输入
注意输出格式
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;


int main(){
    int n;
    double d;
    cin >> n >> d;
    int id;
    while(cin>>id){
        bool disqualified = false;
        int seconds = 0;
        for(int i=0; i!=n; ++i){
            string s;
            cin >> s;
            if(s[0]=='-')
                disqualified = true;
            seconds += (s[0]-'0')*60*60;
            seconds += ((s[2]-'0')*10+(s[3]-'0'))*60;
            seconds += (s[5]-'0')*10+s[6]-'0';
        }
        if(disqualified)
            printf("%3d: -\n", id);
        else{
            double secPerKilo = seconds/d+0.5;
            int minus = secPerKilo/60;
            int secs = (int)(secPerKilo)%60;
            printf("%3d: %d:%02d min/km\n", id, minus, secs);
        }
    }
    return 0;
}
```

