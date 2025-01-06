[링크](https://www.acmicpc.net/problem/14502)

```
#include <bits/stdc++.h>
using namespace std;

const int dy[4] = {-1, 0, 1, 0};
const int dx[4] = {0, 1, 0, -1};
int n, m, a[12][12], visited[12][12], wall = 0, mx = -987654321;
vector<pair<int, int>> v, virus;

void check()
{
    int temp = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (visited[i][j] == 0 && a[i][j] == 0)
                temp++;
        }
    }

    mx = max(mx, temp);
}

void go_virus(int y, int x)
{
    visited[y][x] = 1;

    for (int i = 0; i < 4; i++)
    {
        int ny = y + dy[i];
        int nx = x + dx[i];

        if (ny < 0 || nx < 0 || ny >= n || nx >= m || visited[ny][nx])
            continue;
        if (a[ny][nx] != 0)
            continue;

        go_virus(ny, nx);
    }

    return;
}

int main()
{
    cin >> n >> m;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            cin >> a[i][j];
            if (a[i][j] == 0)
                v.push_back({i, j});
            else if (a[i][j] == 2)
                virus.push_back({i, j});
            else
                wall++;
        }
    }

    for (int i = 0; i < v.size() - 2; i++)
    {
        for (int j = i + 1; j < v.size() - 1; j++)
        {
            for (int k = j + 1; k < v.size(); k++)
            {
                memset(visited, 0, sizeof(visited));
                a[v[i].first][v[i].second] = 1;
                a[v[j].first][v[j].second] = 1;
                a[v[k].first][v[k].second] = 1;

                for (auto vi : virus)
                {
                    go_virus(vi.first, vi.second);
                }

                check();

                a[v[i].first][v[i].second] = 0;
                a[v[j].first][v[j].second] = 0;
                a[v[k].first][v[k].second] = 0;
            }
        }
    }

    cout << mx << "\n";

    return 0;
}
```
