[링크](https://www.acmicpc.net/problem/2979)

```
#include <bits/stdc++.h>
using namespace std;

int a, b, c;
int t[104];
int tin, tout;
int sum = 0;

int main()
{
    cin >> a >> b >> c;

    for (int i = 0; i < 3; i++)
    {
        cin >> tin >> tout;

        for (int i = tin + 1; i <= tout; i++)
        {
            t[i]++;
        }
    }

    for (int i = 1; i <= 100; i++)
    {
        if (t[i] == 1)
        {
            sum += a;
        }
        else if (t[i] == 2)
        {
            sum += b * 2;
        }
        else if (t[i] == 3)
        {
            sum += c * 3;
        }
    }

    cout << sum << "\n";

    return 0;
}
```
