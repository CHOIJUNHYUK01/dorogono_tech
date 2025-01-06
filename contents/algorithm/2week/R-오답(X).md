[링크](https://www.acmicpc.net/problem/1068)

```
#include <bits/stdc++.h>
using namespace std;

int n, rootN, nodeN, delN;
vector<int> adj[54];

int dfs(int here)
{
    int ret = 0;
    int child = 0;

    for (int there : adj[here])
    {
        if (there == delN)
            continue;
        ret += dfs(there);
        child++;
    }

    if (child == 0)
        return 1;
    return ret;
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> nodeN;
        if (nodeN != -1)
        {
            adj[nodeN].push_back(i);
        }
        else
        {
            rootN = i;
        }
    }

    cin >> delN;

    if (delN == rootN)
    {
        cout << 0 << "\n";
        return 0;
    }

    cout << dfs(rootN) << "\n";

    return 0;
}
```
