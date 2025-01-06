[링크](https://www.acmicpc.net/problem/2636)

```
#include <bits/stdc++.h>
using namespace std;

int n, m, c[104], retT, a[104][104], visited[104][104];
int dy[4] = {-1, 0, 1, 0};
int dx[4] = {0, 1, 0, -1};
vector<pair<int, int>> v;

void dfs(int y, int x)
{
    visited[y][x] = 1;

    for (int i = 0; i < 4; i++)
    {
        int ny = dy[i] + y;
        int nx = dx[i] + x;

        if (ny < 0 || nx < 0 || ny >= n || nx >= m)
            continue;
        if (visited[ny][nx])
            continue;
        if (a[ny][nx] == 1)
        {
            v.push_back({ny, nx});
            visited[ny][nx] = 1;
            continue;
        }
        dfs(ny, nx);
    }
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            cin >> a[i][j];
        }
    }

    while (true)
    {
        int leftC = 0;

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                if (a[i][j] == 1)
                    leftC++;
            }
        }

        if (leftC == 0)
            break;
        c[retT] = leftC;

        dfs(0, 0);
        for (auto it : v)
        {
            a[it.first][it.second] = 0;
        }

        v.clear();
        memset(visited, 0, sizeof(visited));
        retT++;
    }

    cout << retT << "\n";
    cout << c[retT - 1] << "\n";

    return 0;
}
```
