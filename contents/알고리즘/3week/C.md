[백준 16234](https://www.acmicpc.net/problem/16234)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

typedef vector<pair<int, int>> v;

int n, l, r, a[54][54], visited[54][54], cnt, ret = 0;
int dy[4] = {-1, 0, 1, 0};
int dx[4] = {0, 1, 0, -1};
v vec;

void bfs(int y, int x)
{
    visited[y][x] = 1;
    vec.push_back({y, x});
    queue<pair<int, int>> q;
    q.push({y, x});
    cnt += a[y][x];

    while (q.size())
    {
        tie(y, x) = q.front();
        q.pop();
        int std = a[y][x];

        for (int i = 0; i < 4; i++)
        {
            int ny = y + dy[i];
            int nx = x + dx[i];

            if (ny < 0 || nx < 0 || ny >= n || nx >= n)
                continue;
            if (visited[ny][nx])
                continue;

            if (abs(a[ny][nx] - std) >= l && abs(a[ny][nx] - std) <= r)
            {
                q.push({ny, nx});
                visited[ny][nx] = 1;
                vec.push_back({ny, nx});
                cnt += a[ny][nx];
            }
        }
    }
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> l >> r;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            cin >> a[i][j];
        }
    }

    while (true)
    {
        int temp = 0;
        bool flag = false;

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (!visited[i][j])
                {
                    // bfs에서 사용될 값 초기화
                    vec.clear();
                    cnt = 0;

                    // 이어진 곳이 조건이 맞다면, 국경을 열어야 하기에 bfs 선택
                    bfs(i, j);
                    if (vec.size() == 1)
                        temp++;

                    // 국경선이 모두 닫힘
                    if (temp == n * n)
                    {
                        flag = true;
                        break;
                    }

                    for (auto it : vec)
                    {
                        a[it.first][it.second] = cnt / vec.size();
                    }
                }
            }
            if (flag)
                break;
        }

        if (flag)
            break;

        memset(visited, 0, sizeof(visited));
        ret++;
    }

    cout << ret << "\n";

    return 0;
}
```
