[링크](https://www.acmicpc.net/problem/14405)

```
#include <bits/stdc++.h>
using namespace std;

string s;
bool flag = false;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> s;
    for (int i = 0; i < s.size(); i++)
    {
        if (i + 1 < s.size() && s[i] == 'p' && s[i + 1] == 'i')
        {
            i += 1;
            continue;
        }

        if (i + 1 < s.size() && s[i] == 'k' && s[i + 1] == 'a')
        {
            i += 1;
            continue;
        }

        if (i + 2 < s.size() && s[i] == 'c' && s[i + 1] == 'h' && s[i + 2] == 'u')
        {
            i += 2;
            continue;
        }

        flag = true;
    }

    if (flag)
        cout << "NO" << "\n";
    else
        cout << "YES" << "\n";

    return 0;
}
```
