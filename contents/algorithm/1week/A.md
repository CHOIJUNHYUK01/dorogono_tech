[링크](https://www.acmicpc.net/problem/2309)

```
#include <bits/stdc++.h>
using namespace std;

int a[9];

int main()
{
    for (int i = 0; i < 9; i++)
    {
        cin >> a[i];
    }

    sort(a, a + 9);

    do
    {
        next_permutation(a, a + 9);
    } while ((accumulate(a, a + 7, 0) != 100));

    for (int i = 0; i < 7; i++)
    {
        cout << a[i] << "\n";
    }

    return 0;
}
```
