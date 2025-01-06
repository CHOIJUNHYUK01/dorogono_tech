[링크](https://www.acmicpc.net/problem/2828)

```
#include <bits/stdc++.h>
using namespace std;

int n, m, j, temp, ret, lf, rf, diff;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m >> j;
    lf = 1;
    rf = m;
    for (int i = 0; i < j; i++)
    {
        cin >> temp;

        if (temp >= lf && temp <= rf)
            continue;

        if (temp < lf)
        {
            diff = lf - temp;
            ret += diff;

            lf = temp;
            rf = lf + m - 1;
        }
        else if (temp > rf)
        {
            diff = temp - rf;
            ret += diff;

            rf = temp;
            lf = rf - m + 1;
        }
    }

    cout << ret << "\n";

    return 0;
}
```
