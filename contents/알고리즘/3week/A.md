[백준 15686](https://www.acmicpc.net/problem/15686)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, m, a[54][54], ret = 987654321;
vector<pair<int, int>> house, chic;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            cin >> a[i][j];
            if (a[i][j] == 1)
            {
                house.push_back({i, j}); // 집 저장
            }
            else if (a[i][j] == 2)
            {
                chic.push_back({i, j}); // 치킨 집 저장
            }
        }
    }

    for (int i = 1; i < (1 << chic.size()); i++)
    {
        vector<pair<int, int>> v;
        for (int j = 0; j < chic.size(); j++)
        {
            if (i & (1 << j))
            {
                v.push_back(chic[j]);
            }
        }

        // 치킨집 개수 제한
        if (v.size() > m)
            continue;

        // 치킨 거리 계산하기
        int cnt = 0;
        for (auto h : house)
        {
            int d = 987654321;
            for (auto c : v)
            {
                int dis = abs(h.first - c.first) + abs(h.second - c.second);

                d = min(d, dis);
            }
            cnt += d;
        }
        ret = min(ret, cnt);
    }

    cout << ret << "\n";

    return 0;
}
```
