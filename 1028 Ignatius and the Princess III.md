# 1028 Ignatius and the Princess III

### Problem Description

```
"Well, it seems the first problem is too easy. I will let you know how foolish you are later." feng5166 says.

"The second problem is, given an positive integer N, we define an equation like this:
  N=a[1]+a[2]+a[3]+...+a[m];
  a[i]>0,1<=m<=N;
My question is how many different equations you can find for a given N.
For example, assume N is 4, we can find:
  4 = 4;
  4 = 3 + 1;
  4 = 2 + 2;
  4 = 2 + 1 + 1;
  4 = 1 + 1 + 1 + 1;
so the result is 5 when N is 4. Note that "4 = 3 + 1" and "4 = 1 + 3" is the same in this problem. Now, you do it!"
```

### **Input**

```
The input contains several test cases. Each test case contains a positive integer N(1<=N<=120) which is mentioned above. The input is terminated by the end of file.
```

### **Output**

```
For each test case, you have to output a line contains an integer P which indicate the different equations you have found.
```

### **Sample Input**

```
4
10
20
```

### **Sample Output**

```
5
42
627
```

### Notes

```C++
母函数通用模板：
	a[0] = 1;
	
	//下面是相乘的过程，代码很难理解!!!
	for(i=1;i<=种类数;++i)             
	{
		memset(b, 0, sizeof(b));
        // n[i] 是第i类的个数，如果是无限个可以省略这个条件
		for(j=0;j<=n[i] && j*v[i]<=MAX;++j)
			for(k=0;k+j*v[i]<=MAX;++k)
				b[k+j*v[i]] += a[k];
		memcpy(a, b, sizeof(b));
	}
```

### Code

```C++
#include<bits/stdc++.h>

using namespace std;

int a[128];
int b[128];

int main(){
    int n;
    while(cin>>n){
        memset(a, 0, sizeof(a));
        a[0] = 1;
        for(int i=1; i<=n; ++i){
            memset(b, 0, sizeof(b));
            for(int j=0; j*i<=n; ++j){
                for(int k=0; k+j*i<=n; ++k){
                    b[k+j*i] += a[k];
                }
            }
            memcpy(a, b, sizeof(b));
        }
        cout << a[n] << endl;
    }
    return 0;
}
```

