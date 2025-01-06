[링크](https://www.acmicpc.net/problem/17298)

```
#include <bits/stdc++.h>
using namespace std;

int n, a[1000004], ret[1000004];
stack<pair<int, int>> stk;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> a[i];
    }

    for (int i = 0; i < n; i++)
    {
        if (stk.empty())
        {
            stk.push({i, a[i]});
            continue;
        }

        while (stk.size() && a[i] > stk.top().second)
        {
            ret[stk.top().first] = a[i];
            stk.pop();
        }

        stk.push({i, a[i]});
    }

    while (stk.size())
    {
        int topIdx = stk.top().first;

        ret[topIdx] = -1;

        stk.pop();
    }

    for (int i = 0; i < n; i++)
    {
        cout << ret[i] << " ";
    }
    cout << "\n";

    return 0;
}
```
