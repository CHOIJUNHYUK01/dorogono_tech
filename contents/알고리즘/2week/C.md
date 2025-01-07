[백준 2468](https://www.acmicpc.net/problem/2468)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, a[104][104], visited[104][104], ret = 1, minN = 101, maxN = 0, rain = 0;
int dy[4] = {-1, 0, 1, 0};
int dx[4] = {0, 1, 0, -1};

void dfs(int y, int x, int maxH)
{
    visited[y][x] = 1;

    for (int i = 0; i < 4; i++)
    {
        int ny = dy[i] + y;
        int nx = dx[i] + x;

        if (ny < 0 || nx < 0 || ny >= n || nx >= n)
            continue;
        if (a[ny][nx] <= maxH)
            continue;
        if (visited[ny][nx])
            continue;

        dfs(ny, nx, maxH);
    }
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            cin >> a[i][j];
            minN = min(a[i][j], minN);
            maxN = max(a[i][j], maxN);
        }
    }

    int temp = 0;
    rain = minN;

    // 비가 최대높이랑 같으면 안전영역 0개임 (의미없음)
    while (rain < maxN)
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (a[i][j] > rain && !visited[i][j])
                {
                    temp++;
                    dfs(i, j, rain); // 구역 세기니까 dfs
                }
            }
        }

        ret = max(ret, temp);

        // 비와서 잠기는 높이가 달라지니까 항상 초기화하고 진행
        rain++;
        temp = 0;
        memset(visited, 0, sizeof(visited));
    }

    cout << ret << "\n";

    return 0;
}
```
