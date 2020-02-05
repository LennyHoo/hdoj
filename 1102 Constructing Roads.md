# 1102 Constructing Roads

### **Problem Description**

```
There are N villages, which are numbered from 1 to N, and you should build some roads such that every two villages can connect to each other. We say two village A and B are connected, if and only if there is a road between A and B, or there exists a village C such that there is a road between A and C, and C and B are connected.

We know that there are already some roads between some villages and your job is the build some roads such that all the villages are connect and the length of all the roads built is minimum.
```

### **Input**

```
The first line is an integer N (3 <= N <= 100), which is the number of villages. Then come N lines, the i-th of which contains N integers, and the j-th of these N integers is the distance (the distance should be an integer within [1, 1000]) between village i and village j.

Then there is an integer Q (0 <= Q <= N * (N + 1) / 2). Then come Q lines, each line contains two integers a and b (1 <= a < b <= N), which means the road between village a and village b has been built.
```

### **Output**

```
You should output a line contains an integer, which is the length of all the roads to be built such that all the villages are connected, and this value is minimum.
```

### **Sample Input**

```
3
0 990 692
990 0 179
692 179 0
1
1 2
```

### **Sample Output**

```
179
```

### Notes

```
克鲁斯卡尔算法，用并查集判断是否有环。
```

### Code

```C++
#include "iostream"
#include "vector"
#include "algorithm"

using namespace std;

struct Edge{
    int start;
    int end;
    int weight;
    explicit Edge() = default;
    explicit Edge(int start, int end, int weight){
        this->start = start;
        this->end = end;
        this->weight = weight;
    }
};

bool cmp(const Edge &a, const Edge &b){
    return (a.weight<b.weight);
}

class DisjointSet{
private:
    vector<int> parent;
public:
    void init(int n){
        this->parent = vector<int>(n+1);
        for(int & t : parent)
            t = -1;
    }
    int findRoot(int x){
        while(parent[x]!=-1){
            x = parent[x];
        }
        return x;
    }
    bool merge(int x, int y){
        int x_root = findRoot(x);
        int y_root = findRoot(y);
        if(x_root==y_root)
            return false;
        else{
            parent[x_root] = y_root;
        }
        return true;
    }
};


int main(){
    int n;
    while(cin>>n){
        vector<Edge> edges;
        vector<int> parent(n+1);
        DisjointSet disjointSet;
        disjointSet.init(n+1);
        for(int i=1; i<=n; ++i){
            for(int j=1; j<=n; ++j){
                int weight;
                cin >> weight;
                if(j>i) edges.emplace_back(Edge(i, j, weight));
            }
        }
        int builtNum;
        cin >> builtNum;
        while(builtNum--){
            int start, end;
            cin >> start >> end;
            disjointSet.merge(start, end);
        }
        sort(edges.begin(), edges.end(), cmp);
        int res = 0;
        for(auto &edge: edges){
            int startRoot = disjointSet.findRoot(edge.start);
            int endRoot = disjointSet.findRoot(edge.end);
            if(startRoot!=endRoot){
                res += edge.weight;
                disjointSet.merge(startRoot, endRoot);
            }
        }
        cout << res << endl;
    }
    return 0;
}
```

