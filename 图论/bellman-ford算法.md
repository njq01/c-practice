# bellman-ford算法

[示例题目](https://www.luogu.com.cn/problem/B3601)

```c++
//bellman_ford算法
#include<iostream>
#include<vector>
#include<cstdio>
using namespace std;
struct node {
    int v, w;
};
long long int f[2003];
vector<node>e[2003];
int main() {
    int n, m;
    cin >> n >> m;
    //邻接表
    for (int i = 0; i < m; i++) {
        int u, v, w;
        cin >> u >> v >> w;
        node x = { v,w };
        e[u].push_back(x);
    }
    f[1] = 0;
    for (int i = 2; i <= n; i++)f[i] = 1000000000000;//初始化
    //主体
    for (int i = 1; i < n; i++) {
        for (int j = 1; j <= n; j++) {
            for (int k = 0; k < e[j].size(); k++)f[e[j][k].v] = min(f[e[j][k].v], f[j] + e[j][k].w);//松弛操作
        }
    }
    //判断有无负环
    int flag = 1;
    for (int i = 1; i < n; i++) {
        for (int j = 1; j <= n; j++) {
            for (int k = 0; k < e[j].size(); k++)if (f[e[j][k].v] > f[j] + e[j][k].w)flag = 0;
        }
    }
    for (int i = 1; i <= n; i++) {
        if (f[i] == 1000000000000)cout << -1 << " ";
        else cout << f[i]<<" ";
    }
    return 0;
}
```