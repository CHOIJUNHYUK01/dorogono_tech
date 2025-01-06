[링크](https://www.acmicpc.net/problem/2178)

```
#include <bits/stdc++.h>
using namespace std;

int n, m, a[104][104], visited[104][104], qy, qx;
int dy[4] = {-1, 0, 1, 0};
int dx[4] = {0, 1, 0, -1};
string s;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m;
    for (int i = 0; i < n; i++)
    {
        cin >> s;
        for (int j = 0; j < s.size(); j++)
        {
            if (s[j] == '1')
            {
                a[i][j] = 1;
            }
            else
            {
                a[i][j] = 0;
            }
        }
    }

    visited[0][0] = 1;
    queue<pair<int, int>> q;
    q.push({0, 0});

    while (q.size())
    {
        tie(qy, qx) = q.front();
        q.pop();

        for (int i = 0; i < 4; i++)
        {
            int ny = dy[i] + qy;
            int nx = dx[i] + qx;

            if (ny < 0 || nx < 0 || ny >= n || nx >= m)
                continue;

            if (a[ny][nx] == 0 || visited[ny][nx] != 0)
                continue;

            visited[ny][nx] = visited[qy][qx] + 1;
            q.push({ny, nx});
        }
    }

    cout << visited[n - 1][m - 1] << "\n";

    return 0;
}
```
