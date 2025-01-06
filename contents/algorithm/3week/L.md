[링크](https://www.acmicpc.net/problem/1987)

```
#include <bits/stdc++.h>
using namespace std;

int n, m, visited[30], ret = 0;
char a[24][24];
vector<int> v;
const int dy[4] = {-1, 0, 1, 0};
const int dx[4] = {0, 1, 0, -1};

void go(int y, int x)
{
    visited[a[y][x] - 'A'] = 1;

    if (v.size())
    {
        int vs = v.size();
        ret = max(ret, vs);
    }

    for (int i = 0; i < 4; i++)
    {
        int ny = dy[i] + y;
        int nx = dx[i] + x;

        if (ny < 0 || nx < 0 || ny >= n || nx >= m)
            continue;
        if (visited[a[ny][nx] - 'A'])
            continue;
        visited[a[ny][nx] - 'A'] = 1;
        v.push_back(a[ny][nx] - 'A');

        go(ny, nx);

        visited[a[ny][nx] - 'A'] = 0;
        v.pop_back();
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

    v.push_back((a[0][0] - 'A'));
    go(0, 0);

    cout << ret << "\n";

    return 0;
}
```
