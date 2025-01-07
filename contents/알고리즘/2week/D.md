[백준 2583](https://www.acmicpc.net/problem/2583)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, m, k, a[104][104], visited[104][104], area, sizeA;
int bx, by, tx, ty;
int dy[4] = {-1, 0, 1, 0};
int dx[4] = {0, 1, 0, -1};
vector<int> v;

int dfs(int y, int x)
{
    // 실행마다 size가 늘어나도록 설정
    visited[y][x] = 1;
    sizeA++;

    for (int i = 0; i < 4; i++)
    {
        int ny = dy[i] + y;
        int nx = dx[i] + x;

        if (ny < 0 || nx < 0 || ny >= n || nx >= m)
            continue;
        if (a[ny][nx] || visited[ny][nx])
            continue;

        dfs(ny, nx);
    }

    return sizeA;
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m >> k;
    for (int i = 0; i < k; i++)
    {
        cin >> bx >> by >> tx >> ty;

        // 박스 구역 칠하기
        for (int j = by; j < ty; j++)
        {
            for (int l = bx; l < tx; l++)
            {
                a[j][l] = 1;
            }
        }
    }

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (a[i][j] == 1 || visited[i][j])
                continue;

            // 구역 개수와 설정을 vector로 해결
            v.push_back(dfs(i, j));
            sizeA = 0;
            area++;
        }
    }

    sort(v.begin(), v.end());
    cout << area << "\n";
    for (auto i : v)
    {
        cout << i << " ";
    }
    cout << "\n";

    return 0;
}
```
