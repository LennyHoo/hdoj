# 1162 Eddy's picture

### **Problem Description**

```
Eddy begins to like painting pictures recently ,he is sure of himself to become a 
painter.Every day Eddy draws pictures in his small room, and he usually puts out his 
newest pictures to let his friends appreciate. but the result it can be imagined, the 
friends are not interested in his picture.Eddy feels very puzzled,in order to change 
all friends 's view to his technical of painting pictures ,so Eddy creates a problem 
for the his friends of you.
Problem descriptions as follows: Given you some coordinates pionts on a drawing paper, 
every point links with the ink with the straight line, causes all points finally to 
link in the same place. How many distants does your duty discover the shortest length which the ink draws?
```

### **Input**

```
The first line contains 0 < n <= 100, the number of point. For each point, a line 
follows; each following line contains two real numbers indicating the (x,y) 
coordinates of the point.

Input contains multiple test cases. Process to the end of file.
```

### **Output**

```
Your program prints a single real number to two decimal places: the minimum total 
length of ink lines that can connect all the points.
```

### **Sample Input**

```
3
1.0 1.0
2.0 2.0
2.0 4.0
```

### **Sample Output**

```
3.41
```

### Notes

```
Kruskal + DisjointSet
```

### Code

```C++
#include "bits/stdc++.h"

using namespace std;


struct Edge{
    int start;
    int end;
    double weight;
    explicit Edge() = default;
    explicit Edge(int start, int end, double weight){
        this->start = start;
        this->end = end;
        this->weight = weight;
    }
};

struct Node{
    double x;
    double y;
    explicit Node() = default;
    explicit Node(double x, double y){
        this->x = x;
        this->y = y;
    }
};

double length(const Node &a, const Node &b){
    return sqrt(pow(a.x-b.x, 2)+pow(a.y-b.y, 2));
}

class DisjointSet{
private:
    vector<int> parent;
public:
    void init(int n){
        parent = vector<int>(n, -1);
    }
    int findRoot(int x){
        while(parent[x]!=-1)
            x = parent[x];
        return x;
    }
    bool merge(int x, int y){
        int x_root = findRoot(x);
        int y_root = findRoot(y);
        if(x_root==y_root)
            return false;
        else{
            parent[x_root] = y_root;
            return true;
        }
    }
};

bool cmp(const Edge &a, const Edge &b){
    return (a.weight<b.weight);
}

int main(){
    int n;
    while(cin>>n){
        vector<Node> nodes;
        vector<Edge> edges;
        DisjointSet disjointSet;
        disjointSet.init(n);
        for(int i=0; i<n; ++i){
            double x, y;
            cin >> x >> y;
            Node node = Node(x, y);
            nodes.emplace_back(node);
            for(int j=0; j<=i-1; ++j){
                edges.emplace_back(Edge(j, i, length(nodes[j], node)));
            }
        }
        sort(edges.begin(), edges.end(), cmp);
        double res = 0;
        for(auto &edge: edges){
            int stRoot = disjointSet.findRoot(edge.start);
            int endRoot = disjointSet.findRoot(edge.end);
            if(stRoot!=endRoot){
                res += edge.weight;
                disjointSet.merge(stRoot, endRoot);
            }
        }
        printf("%.2lf\n", res);
    }
    return 0;
}
```

