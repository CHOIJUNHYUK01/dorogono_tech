[링크](https://www.acmicpc.net/problem/2559)

```
#include <bits/stdc++.h>
using namespace std;

int n, k, temp, psum[100004], ret;

int main()
{
    cin >> n >> k;

    for (int i = 0; i < n; i++)
    {
        cin >> temp;

        if (i != 0)
        {
            psum[i] = temp + psum[i - 1];
        }
        else
        {
            psum[i] = temp;
        }
    }

    ret = psum[k - 1];

    for (int i = k; i < n; i++)
    {
        ret = max(ret, psum[i] - psum[i - k]);
    }

    cout << ret << "\n";

    return 0;
}
```
