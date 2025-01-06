[링크](https://www.acmicpc.net/problem/1094)

```
#include <bits/stdc++.h>
using namespace std;

int x = 64, n, cnt = 0;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;

    while (n != 0)
    {
        if (x > n)
        {
            x = x >> 1;
            continue;
        }

        n -= x;
        cnt++;
    }

    cout << cnt << "\n";

    return 0;
}
```
