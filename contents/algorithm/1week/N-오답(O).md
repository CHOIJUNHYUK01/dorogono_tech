[링크](https://www.acmicpc.net/problem/1629)

```
#include <bits/stdc++.h>
using namespace std;

int a, b, c;

int go(int n)
{
    if (n == 1)
        return a % c;

    long long ret = go(n / 2);
    ret = (ret * ret) % c;

    if (n % 2)
        ret = (ret * a) % c;

    return ret;
}

int main()
{
    cin >> a >> b >> c;

    cout << go(b) << "\n";

    return 0;
}
```
