# 1088 Write a simple HTML Browser

### **Problem Description**

```
If you ever tried to read a html document on a Macintosh, you know how hard it is if no Netscape is installed.
Now, who can forget to install a HTML browser? This is very easy because most of the times you don't need one on a MAC because there is a Acrobate Reader which is native to MAC. But if you ever need one, what do you do?
Your task is to write a small html-browser. It should only display the content of the input-file and knows only the html commands (tags) <br> which is a linebreak and <hr> which is a horizontal ruler. Then you should treat all tabulators, spaces and newlines as one space and display the resulting text with no more than 80 characters on a line.
```

### **Input**

```
The input consists of a text you should display. This text consists of words and HTML tags separated by one or more spaces, tabulators or newlines.
A word is a sequence of letters, numbers and punctuation. For example, "abc,123" is one word, but "abc, 123" are two words, namely "abc," and "123". A word is always shorter than 81 characters and does not contain any '<' or '>'. All HTML tags are either <br> or <hr>.
```

### **Output**

```
You should display the the resulting text using this rules:
  . If you read a word in the input and the resulting line does not get longer than 80 chars, print it, else print it on a new line.
  . If you read a <br> in the input, start a new line.
  . If you read a <hr> in the input, start a new line unless you already are at the beginning of a line, display 80 characters of '-' and start a new line (again).
The last line is ended by a newline character.
```

### **Sample Input**

```
Hallo, dies ist eine 
ziemlich lange Zeile, die in Html
aber nicht umgebrochen wird.
<br>
Zwei <br> <br> produzieren zwei Newlines. 
Es gibt auch noch das tag <hr> was einen Trenner darstellt.
Zwei <hr> <hr> produzieren zwei Horizontal Rulers.
Achtung       mehrere Leerzeichen irritieren

Html genauso wenig wie


mehrere Leerzeilen.
```

### **Sample Output**

```
Hallo, dies ist eine ziemlich lange Zeile, die in Html aber nicht umgebrochen
wird.
Zwei

produzieren zwei Newlines. Es gibt auch noch das tag
--------------------------------------------------------------------------------
was einen Trenner darstellt. Zwei
--------------------------------------------------------------------------------
--------------------------------------------------------------------------------
produzieren zwei Horizontal Rulers. Achtung mehrere Leerzeichen irritieren Html
genauso wenig wie mehrere Leerzeilen.
```

### Notes

```
每次输入一个词，就立即处理，直到文件末尾。
（1） 每行最多80个字符，如果加上最后一个单词大于80，则最后一个单词移到下一行。
（2） <hr>如果处于当前行字符数等于0的情况，则直接输出，否则先输出回车，在输出<hr>
（3） 文章最后要有一个回车
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;


int main(){
    string word;
    int count = 0;
    while(cin>>word){
        if(word=="<br>"){
            cout << endl;
            count = 0;
        }
        else if(word=="<hr>"){
            if(!count)
                cout << "--------------------------------------------------------------------------------" << endl;
            else{
                cout << endl
                     << "--------------------------------------------------------------------------------" << endl;
            }
            count = 0;
        }
        else{
            if(!count){
                count = word.size();
                cout << word;
            }
            else if(count+word.size()+1>80){
                cout << endl << word;
                count = word.size();
            }
            else{
                cout << " " << word;
                count += word.size() + 1;
            }
        }
    }
    cout << endl;
    return 0;
}
```

