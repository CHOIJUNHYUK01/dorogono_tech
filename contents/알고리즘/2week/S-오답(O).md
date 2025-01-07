[백준 1325](https://www.acmicpc.net/problem/1325)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, m, a, b, visited[10004], h[10004], mx = -987654321;
vector<int> adj[10004];

int dfs(int here)
{
    visited[here] = 1;
    int ret = 1;

    for (int there : adj[here])
    {
        if (visited[there])
            continue;
        ret += dfs(there);
    }

    return ret;
}

int main()
{
    cin >> n >> m;
    for (int i = 0; i < m; i++)
    {
        cin >> a >> b;
        adj[b].push_back(a);
    }

    for (int i = 1; i <= n; i++)
    {
        // 각 컴퓨터마다 겹치는 컴퓨터도 있으니 초기화할 것
        memset(visited, 0, sizeof(visited));
        h[i] = dfs(i);
        mx = max(mx, h[i]);
    }

    for (int i = 1; i <= n; i++)
    {
        if (mx == h[i])
            cout << i << " ";
    }
    cout << "\n";

    return 0;
}
```
