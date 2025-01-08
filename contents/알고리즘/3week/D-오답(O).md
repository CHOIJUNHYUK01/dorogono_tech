[백준 4179](https://www.acmicpc.net/problem/4179)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

const int INF = 987654321;
int dy[4] = {-1, 0, 1, 0};
int dx[4] = {0, 1, 0, -1};
int n, m, ret, fire[1004][1004], visited[1004][1004], y, x;
pair<int, int> start;
vector<pair<int, int>> f;
char a[1004][1004];

void move_start()
{
    queue<pair<int, int>> q;
    q.push(start);
    visited[start.first][start.second] = 1;

    while (q.size())
    {
        tie(y, x) = q.front();
        q.pop();

        if (y == 0 || x == 0 || y == n - 1 || x == m - 1)
        {
            ret = visited[y][x];
            break;
        }

        for (int i = 0; i < 4; i++)
        {
            int ny = y + dy[i];
            int nx = x + dx[i];

            // 범위 체크
            if (ny < 0 || nx < 0 || ny >= n || nx >= m)
                continue;
            // 벽 못감
            if (a[ny][nx] == '#')
                continue;
            // 이미 간 곳
            if (visited[ny][nx])
                continue;
            // 불보다 늦게 간 곳
            if (visited[y][x] + 1 >= fire[ny][nx])
                continue;

            visited[ny][nx] = visited[y][x] + 1;
            q.push({ny, nx});
        }
    }
}

void fire_spread()
{
    queue<pair<int, int>> q;
    for (auto it : f)
    {
        q.push(it);
        fire[it.first][it.second] = 1;
    }

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
            if (fire[ny][nx] != INF)
                continue;
            if (a[ny][nx] == '#')
                continue;

            fire[ny][nx] = fire[y][x] + 1;
            q.push({ny, nx});
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
            if (a[i][j] == 'J')
            {
                start = {i, j};
                a[i][j] = '.';
            }
            if (a[i][j] == 'F')
                f.push_back({i, j});
        }
    }

    // 불이 도달한 시간보다 늦으면 못가니까 최댓값으로 설정함
    // 불이 없을 때, 초기값이 0이라면 지훈이가 못 움직임
    fill(&fire[0][0], &fire[0][0] + 1004 * 1004, INF);
    fire_spread();

    move_start();

    if (ret)
        cout << ret << "\n";
    else
        cout << "IMPOSSIBLE" << "\n";

    return 0;
}
```
