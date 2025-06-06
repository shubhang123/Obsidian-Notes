#dfs  dfs template for every dfs question
  
  ```cpp
  #include <bits/stdc++.h>
using namespace std;
const int N = 1e5 + 10;

vector<int> g[N];
bool vis[N];

void dfs(int vertex) {
    /* Take action on vertex after entering
       the vertex
    */
    vis[vertex] = true;
    for (int child : g[vertex]) {
        if (vis[child]) continue;
        /*Take action on child before
          entering the child node for dfs
        */
        dfs(child);
        /*Take action on child
        after exiting the child node
        */
    }
    /*Take action on vertex before
    exiting the vertex
    */
}
int main() {
    int v, e;
    cin >> v >> e;
    for (int i = 0; i < e; i++) {
        int v1, v2;
        cin >> v1 >> v2;
        g[v1].push_back(v2);
        g[v2].push_back(v1);
    }
    dfs(1);
    return 0;
}

```