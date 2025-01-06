[링크](https://www.acmicpc.net/problem/14497)

```
#include <bits/stdc++.h>
using namespace std;

int n, m, visited[304][304], ret, sy, sx, fy, fx;
char a[304][304];
const int dy[4] = {-1, 0, 1, 0};
const int dx[4] = {0, 1, 0, -1};
vector<pair<int, int>> v;

void go(int y, int x)
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

        if (a[ny][nx] == '1')
        {
            visited[ny][nx] = 1;
            v.push_back({ny, nx});
            continue;
        }
        else if (a[ny][nx] == '#')
        {
            visited[ny][nx] = 1;
            a[ny][nx] = 'X';
            return;
        }
        else if (a[ny][nx] == '0')
        {
            go(ny, nx);
        }
    }
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m >> sy >> sx >> fy >> fx;
    sy--;
    sx--;
    fy--;
    fx--;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            cin >> a[i][j];
        }
    }

    while (a[fy][fx] != 'X')
    {
        ret++;
        memset(visited, 0, sizeof(visited));
        v.clear();

        go(sy, sx);
        for (auto it : v)
        {
            a[it.first][it.second] = '0';
        }
    }

    cout << ret << "\n";

    return 0;
}
```
