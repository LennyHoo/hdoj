# 1079 Calendar Game

### Calendar Game

```
Adam and Eve enter this year’s ACM International Collegiate Programming Contest. Last night, they played the Calendar Game, in celebration of this contest. This game consists of the dates from January 1, 1900 to November 4, 2001, the contest day. The game starts by randomly choosing a date from this interval. Then, the players, Adam and Eve, make moves in their turn with Adam moving first: Adam, Eve, Adam, Eve, etc. There is only one rule for moves and it is simple: from a current date, a player in his/her turn can move either to the next calendar date or the same day of the next month. When the next month does not have the same day, the player moves only to the next calendar date. For example, from December 19, 1924, you can move either to December 20, 1924, the next calendar date, or January 19, 1925, the same day of the next month. From January 31 2001, however, you can move only to February 1, 2001, because February 31, 2001 is invalid.

A player wins the game when he/she exactly reaches the date of November 4, 2001. If a player moves to a date after November 4, 2001, he/she looses the game.

Write a program that decides whether, given an initial date, Adam, the first mover, has a winning strategy.

For this game, you need to identify leap years, where February has 29 days. In the Gregorian calendar, leap years occur in years exactly divisible by four. So, 1993, 1994, and 1995 are not leap years, while 1992 and 1996 are leap years. Additionally, the years ending with 00 are leap years only if they are divisible by 400. So, 1700, 1800, 1900, 2100, and 2200 are not leap years, while 1600, 2000, and 2400 are leap years.
```

### **Input**

```
The input consists of T test cases. The number of test cases (T) is given in the first line of the input. Each test case is written in a line and corresponds to an initial date. The three integers in a line, YYYY MM DD, represent the date of the DD-th day of MM-th month in the year of YYYY. Remember that initial dates are randomly chosen from the interval between January 1, 1900 and November 4, 2001.
```

### **Output**

```
Print exactly one line for each test case. The line should contain the answer "YES" or "NO" to the question of whether Adam has a winning strategy against Eve. Since we have T test cases, your program should output totally T lines of "YES" or "NO".
```

### **Sample Input**

```
3 
2001 11 3 
2001 11 2 
2001 10 3 
```

### **Sample Output**

```
YES 
NO 
NO 
```

### Notes

```
把月和日的和看做一个数a，那么两个人依次决定后会改变a的奇偶性；
最后面对11,4（a=11+4）是一个奇数，所以谁面对奇数这个状态谁就输了；
反过来说如果谁把对方控制每次都是奇数，必然赢，在所有的日期中，所有的a是偶数的月份肯定可以只用一步就把对方控制成奇数，（****9.30，和11.30 也可以）让对方一直是奇数包括平年或闰年的2月都一样；
所以最先抢到a是偶数或者9.30或11.30的人会赢，也就是说第一个人面对的输入值a=(月+日)不满足赢的状态，那么他一定会输；
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;

int daysNum[] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

bool isLeapYear(int year){
    return (year%4==0&&year%100!=0)||year%400==0;
}

vector<int> nextDay(const vector<int> &today){
    int thisYear = today[0];
    int thisMonth = today[1];
    int thisDay = today[2];
    int year = thisYear, month = thisMonth, day = thisDay;
    if(isLeapYear(thisYear))
        daysNum[2] = 29;
    else
        daysNum[2] = 28;
    if(thisDay>=daysNum[thisMonth]){
        day = 1;
        if(thisMonth==12){
            month = 1;
            year = thisYear + 1;
        }
        else
            month = thisMonth + 1;
    }
    else
        day = thisDay + 1;
    vector<int> res = {year, month, day};
    return res;
}

vector<int> sameDayNextMonth(const vector<int> &today){
    int thisYear = today[0];
    int thisMonth = today[1];
    int thisDay = today[2];
    int year = thisYear, month, day = thisDay;
    if(isLeapYear(thisYear))
        daysNum[2] = 29;
    else
        daysNum[2] = 28;
    if(thisMonth==12){
        month = 1;
        year = thisYear + 1;
    }
    else
        month = thisMonth + 1;
    vector<int> res;
    if(daysNum[month]>=thisDay){
        res.emplace_back(year);
        res.emplace_back(month);
        res.emplace_back(day);
    }
    return res;
}

typedef enum{Adam, Eve} Player_t;


struct Node{
    Player_t player;
    vector<int> day;
    Node(Player_t player, const vector<int> &day){
        this->player = player;
        this->day = day;
    }
};

struct cmp{
    bool operator()(Node a, Node b){
        if(a.day[0]<b.day[0])
            return true;
        else if(a.day[0]==b.day[0]){
            if(a.day[1]<b.day[1])
                return true;
            else if(a.day[1]==b.day[1]){
                return a.day[2]<b.day[2];
            }
            else
                return false;
        }
        else
            return false;
    }
};

bool legal(const vector<int> &day){
    if(day[0]>2001) return false;
    if(day[0]==2001&&day[1]>11) return false;
    return !(day[0] == 2001 && day[1] == 11 && day[2] > 4);
}

bool bfs(const vector<int> &startDay){
    priority_queue<Node, vector<Node>, cmp> Q;
    Q.push(Node(Eve, startDay));
    while(!Q.empty()){
        Node node = Q.top();
        if(node.player==Adam&&node.day[0]==2001&&node.day[1]==11&&node.day[2]==4)
            return true;
        if(node.player==Eve&&node.day[0]==2001&&node.day[1]==11&&node.day[2]==4)
            return false;
        Q.pop();
        vector<int> nextCalendarDay;
        vector<int> sameNextMonthDay;
        switch(node.player){
            case Adam:
                nextCalendarDay = nextDay(node.day);
                sameNextMonthDay = sameDayNextMonth(node.day);
                if(legal(nextCalendarDay))
                    Q.push(Node(Eve, nextCalendarDay));
                if(!sameNextMonthDay.empty()&&legal(sameNextMonthDay))
                    Q.push(Node(Eve, sameNextMonthDay));
                break;
            case Eve:
                nextCalendarDay = nextDay(node.day);
                sameNextMonthDay = sameDayNextMonth(node.day);
                if(legal(nextCalendarDay))
                    Q.push(Node(Adam, nextCalendarDay));
                if(!sameNextMonthDay.empty()&&legal(sameNextMonthDay))
                    Q.push(Node(Adam, sameNextMonthDay));
                break;
        }
    }
    return false;
}


int main(){
    int n;
    cin >> n;
    while(n--){
        int year, month, day;
        cin >> year >> month >> day;
        if((month==9&&day==30)||(month==11&&day==30)){
            cout << "YES" << endl;
            continue;
        }
        vector<int> startDay;
        startDay.emplace_back(year);
        startDay.emplace_back(month);
        startDay.emplace_back(day);
        if(bfs(startDay))
            cout << "YES" << endl;
        else
            cout << "NO" << endl;
    }
    return 0;
}
```

