[링크](https://www.acmicpc.net/problem/1992)

```
#include <bits/stdc++.h>
using namespace std;

int n;
string s;
char a[68][68];

string go(int y, int x, int size)
{
    if (size == 1)
        return string(1, a[y][x]);

    char std = a[y][x];
    string ret = "";
    for (int i = y; i < y + size; i++)
    {
        for (int j = x; j < x + size; j++)
        {
            if (a[i][j] != std)
            {
                ret += '(';
                ret += go(y, x, size / 2);
                ret += go(y, x + size / 2, size / 2);
                ret += go(y + size / 2, x, size / 2);
                ret += go(y + size / 2, x + size / 2, size / 2);
                ret += ')';

                return ret;
            }
        }
    }

    return string(1, std);
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> s;
        for (int j = 0; j < n; j++)
        {
            a[i][j] = s[j];
        }
    }

    cout << go(0, 0, n) << "\n";

    return 0;
}
```
