[링크](https://www.acmicpc.net/problem/12869)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int att[6][3] = {
    {1, 3, 9},
    {1, 9, 3},
    {3, 1, 9},
    {3, 9, 1},
    {9, 1, 3},
    {9, 3, 1},
};

int n, scv[3], ret, visited[64][64][64], a, b, c;
queue<tuple<int, int, int>> q;

void bfs()
{
    q.push({scv[0], scv[1], scv[2]});
    visited[scv[0]][scv[1]][scv[2]] = 1;

    while (q.size())
    {
        tie(a, b, c) = q.front();
        q.pop();

        if (a == 0 && b == 0 && c == 0)
            break;

        for (int i = 0; i < 6; i++)
        {
            // 0은 이미 죽은 것이니 0보다 떨어질 수 없음
            int na = max(0, a - att[i][0]);
            int nb = max(0, b - att[i][1]);
            int nc = max(0, c - att[i][2]);

            if (visited[na][nb][nc])
                continue;

            visited[na][nb][nc] = visited[a][b][c] + 1;
            q.push({na, nb, nc});
        }
    }
}

int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> scv[i];
    }

    // 각 공격 회수에 따라 체력이 결정되니까 bfs 선택함
    bfs();

    cout << visited[0][0][0] - 1 << "\n";

    return 0;
}
```
