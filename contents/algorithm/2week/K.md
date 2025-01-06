[링크](https://www.acmicpc.net/problem/3474)

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
        // 5의 배수 개수
        for (int i = 5; i <= n; i *= 5)
        {
            ret += (n / i);
        }

        cout << ret << "\n";
    }

    return 0;
}
```
