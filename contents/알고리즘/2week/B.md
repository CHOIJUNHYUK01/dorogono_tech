[백준 1012](https://www.acmicpc.net/problem/1012)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int t, n, m, k, by, bx, a[2504][2504], visited[2504][2504], ret;
int dy[4] = {-1, 0, 1, 0};
int dx[4] = {0, 1, 0, -1};

void go(int y, int x)
{
    visited[y][x] = 1;

    for (int i = 0; i < 4; i++)
    {
        int ny = y + dy[i];
        int nx = x + dx[i];

        if (ny < 0 || nx < 0 || ny >= n || nx >= m)
            continue;
        if (a[ny][nx] == 0 || visited[ny][nx])
            continue;

        go(ny, nx);
    }
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> t;

    while (t--)
    {
        cin >> m >> n >> k;
        for (int i = 0; i < k; i++)
        {
            cin >> bx >> by;
            a[by][bx] = 1;
        }

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                if (a[i][j] && !visited[i][j])
                {
                    ret++;
                    go(i, j); // 땅이 연결됐는지만 확인하기 위한 dfs 선택
                }
            }
        }

        cout << ret << "\n";

        // 초기화가 제일 중요!!
        ret = 0;
        memset(a, 0, sizeof(a));
        memset(visited, 0, sizeof(visited));
    }

    return 0;
}
```
