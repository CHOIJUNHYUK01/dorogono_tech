[백준 4375](https://www.acmicpc.net/problem/4375)

<img src="https://skillicons.dev/icons?i=cpp" />

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

        // 1, 11, 111 ... 하면서 나머지값으로 확인
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
