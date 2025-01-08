[백준 2589](https://www.acmicpc.net/problem/2589)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, m, visited[54][54], ret = 0;
char a[54][54];
const int dy[4] = {-1, 0, 1, 0};
const int dx[4] = {0, 1, 0, -1};

void bfs(int y, int x)
{
    visited[y][x] = 0;
    queue<pair<int, int>> q;
    q.push({y, x});

    while (q.size())
    {
        tie(y, x) = q.front();
        q.pop();

        for (int i = 0; i < 4; i++)
        {
            int ny = y + dy[i];
            int nx = x + dx[i];

            if (ny < 0 || nx < 0 || ny >= n || nx >= m)
                continue;
            if (visited[ny][nx] != -1)
                continue;
            if (a[ny][nx] == 'W')
                continue;

            visited[ny][nx] = visited[y][x] + 1;
            q.push({ny, nx});
            ret = max(ret, visited[ny][nx]);
        }
    }
}

int main()
{
    cin >> n >> m;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            cin >> a[i][j];
        }
    }

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            // 어차피 순회하니, 땅이 겹쳐서 중복될 일은 없음
            if (a[i][j] == 'L')
            {
                // 해당 시작점에서 체크하니까 초기화할 것
                memset(visited, -1, sizeof(visited));
                // 위나 아래로 이동할 경우에 모두 +1값이니까 bfs 선택
                bfs(i, j);
            }
        }
    }

    cout << ret << "\n";

    return 0;
}
```
