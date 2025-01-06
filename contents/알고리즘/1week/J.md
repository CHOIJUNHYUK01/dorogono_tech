[링크](https://www.acmicpc.net/problem/9375)

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
        mp.clear();
        ret = 1;

        for (int j = 0; j < n; j++)
        {
            cin >> c1 >> c2;
            mp[c2]++;
        }

        for (auto it : mp)
        {
            ret *= (it.second + 1);
        }

        cout << ret - 1 << "\n";
    }

    return 0;
}
```
