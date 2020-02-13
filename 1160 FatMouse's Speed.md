# 1160 FatMouse's Speed

### **Problem Description**

```
http://acm.hdu.edu.cn/showproblem.php?pid=1160
```

### Notes

```
lis + 反向记录路径
```

### Code

```c++
#include "bits/stdc++.h"

using namespace std;

struct Mouse{
    int weight;
    int speed;
    int index;
    Mouse *pre;
    explicit Mouse(int weight=0, int speed=0, int index=0, Mouse *pre=nullptr){
        this->weight = weight;
        this->speed = speed;
        this->index = index;
        this->pre = pre;
    }
};

bool cmpWeight(Mouse *a, Mouse *b){
    return (a->weight>b->weight);
}

int binarySearch(const vector<Mouse*> helper, Mouse *mouse, int len){
    int low = 1;
    int high = len;
    while(low<=high){
        int mid = (low+high)/2;
        if(helper[mid]->speed>mouse->speed)
            high = mid - 1;
        else if(helper[mid]->speed<mouse->speed)
            low = mid + 1;
        else 
            return mid;
    }
    return low;
}

pair<int, Mouse*> lis(const vector<Mouse*> &mouses){
    int len = 1;
    int n = mouses.size();
    vector<Mouse*> helper(n+1);
    helper[1] = mouses[0];
    for(int i=1; i<n; ++i){
        if(mouses[i]->speed>helper[len]->speed){
            mouses[i]->pre = helper[len];
            helper[++len] = mouses[i];
        }
        else{
            int pos = binarySearch(helper, mouses[i], len);
            mouses[i]->pre = helper[pos-1];
            helper[pos] = mouses[i];
        }
    }
    return make_pair(len, helper[len]);
}



int main()
{
    int weight, speed;
    vector<Mouse*> mouses;
    int index = 1;
    while(cin>>weight>>speed){
        Mouse *newMouse = new Mouse(weight, speed, index++);
        mouses.emplace_back(newMouse);
    }
    if(index==1){
        printf("0\n");
        return 0;
    }
    sort(mouses.begin(), mouses.end(), cmpWeight);
    pair<int, Mouse*> res = lis(mouses);
    printf("%d\n", res.first);
    Mouse *pointer = res.second;
    while(pointer!=nullptr){
        printf("%d\n", pointer->index);
        pointer = pointer->pre;
    }
    for(auto &p: mouses)   
        delete p;
    return 0;
}
```

