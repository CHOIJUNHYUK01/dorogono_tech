[백준 3474](https://www.acmicpc.net/problem/3474)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int t, n;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> t;

    while (t--)
    {
        cin >> n;

        int ret = 0;

        // 0이 나오는 경우는 10의 배수, 즉 2 * 5임.
        // 5의 배수 개수만 세면 됨
        for (int i = 5; i <= n; i *= 5)
        {
            ret += (n / i);
        }

        cout << ret << "\n";
    }

    return 0;
}
```
