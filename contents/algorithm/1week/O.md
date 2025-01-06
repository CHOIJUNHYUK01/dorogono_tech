[링크](https://www.acmicpc.net/problem/4375)

```
#include <bits/stdc++.h>
using namespace std;

int n;

int main()
{
    while (cin >> n)
    {
        int ret = 1;
        int ex = 1;

        if (n == 1)
        {
            cout << ret << "\n";
            continue;
        }

        while (ex)
        {
            ret++;
            ex = ex * 10 + 1;
            ex %= n;
        }

        cout << ret << "\n";
    }

    return 0;
}
```
