[링크](https://www.acmicpc.net/problem/1940)

```
#include <bits/stdc++.h>
using namespace std;

int n, m, a[15004], ret;

int main()
{
    cin >> n >> m;
    for (int i = 0; i < n; i++)
    {
        cin >> a[i];
    }

    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            if (a[i] + a[j] == m)
                ret++;
        }
    }

    cout << ret << "\n";

    return 0;
}
```
