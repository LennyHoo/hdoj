# 1085 Holding Bin-Laden Captive!

### **Problem Description**

```
We all know that Bin-Laden is a notorious terrorist, and he has disappeared for a long time. But recently, it is reported that he hides in Hang Zhou of China!
“Oh, God! How terrible! ”

Don’t be so afraid, guys. Although he hides in a cave of Hang Zhou, he dares not to go out. Laden is so bored recent years that he fling himself into some math problems, and he said that if anyone can solve his problem, he will give himself up!
Ha-ha! Obviously, Laden is too proud of his intelligence! But, what is his problem?
“Given some Chinese Coins (硬币) (three kinds-- 1, 2, 5), and their number is num_1, num_2 and num_5 respectively, please output the minimum value that you cannot pay with given coins.”
You, super ACMer, should solve the problem easily, and don’t forget to take $25000000 from Bush!
```

### **Input**

```
Input contains multiple test cases. Each test case contains 3 positive integers num_1, num_2 and num_5 (0<=num_i<=1000). A test case containing 0 0 0 terminates the input and this test case is not to be processed.
```

### **Output**

```
Output the minimum positive value that one cannot pay with given coins, one line for one case.
```

### **Sample Input**

```
1 1 3
0 0 0
```

### **Sample Output**

```
4
```

### Notes

```C++
母函数模板：
	memset(a, 0, sizeof(a));
        a[0] = 1;
        for(int i=0; i<种类数; ++i){
            memset(b, 0, sizeof(b));
            for(int j=0; j<=num[i]&&j*value[i]<N; ++j){
                for(int k=0; k<N&&k+j*value[i]<N; ++k)
                    b[k+j*value[i]] += a[k];
            }
            memcpy(a, b, sizeof(b));
        }
```

