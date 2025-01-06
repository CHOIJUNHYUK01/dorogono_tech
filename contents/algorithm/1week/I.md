[링크](https://www.acmicpc.net/problem/1620)

```
#include <bits/stdc++.h>
using namespace std;

map<int, string> mp;
map<string, int> mp2;
int n, m;
string s, q;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        cin >> s;
        mp[i] = s;
        mp2[s] = i;
    }

    for (int i = 0; i < m; i++)
    {
        cin >> q;
        if (atoi(q.c_str()) == 0)
        {
            cout << mp2[q] << "\n";
        }
        else
        {
            cout << mp[atoi(q.c_str())] << "\n";
        }
    }

    return 0;
}
```
