[백준 9375](https://www.acmicpc.net/problem/9375)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int t, n, ret;
string c1, c2;
map<string, int> mp;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> t;
    for (int i = 0; i < t; i++)
    {
        cin >> n;

        // 새로운 문제니까 초기화
        mp.clear();
        ret = 1;

        for (int j = 0; j < n; j++)
        {
            cin >> c1 >> c2;

            // 카테고리만 신경쓰면 됨
            mp[c2]++;
        }

        for (auto it : mp)
        {
            // 개수에 +1은 안 입는다는 것 포함
            ret *= (it.second + 1);
        }

        // 다 안입는 경우의 수 1을 뺌
        cout << ret - 1 << "\n";
    }

    return 0;
}
```
