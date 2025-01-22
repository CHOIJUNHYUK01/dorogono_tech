[링크](https://www.acmicpc.net/problem/14497)

<img src="https://skillicons.dev/icons?i=cpp" />

```cpp
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
            // 사람이 있으면 멈춰야 하기에 방문체크만 함
            // 벡터에는 추후에 0으로 바꿔야 함
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

    // 본인은 0,0을 시작점으로 할 것이기에 뺐음
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
        // 점프 수
        ret++;
        // 파동 확인 배열 초기화
        memset(visited, 0, sizeof(visited));
        v.clear();

        go(sy, sx);

        // 점프를 맞은 친구는 0으로 바꿈
        for (auto it : v)
        {
            a[it.first][it.second] = '0';
        }
    }

    cout << ret << "\n";

    return 0;
}

```
