[링크](https://www.acmicpc.net/problem/10988)

```
#include <bits/stdc++.h>
using namespace std;

string s;
int ret = 1;

int main()
{
    cin >> s;

    for (int i = 0; i < s.size() / 2; i++)
    {
        if (s[i] != s[s.size() - i - 1])
        {
            ret = 0;
            break;
        }
    }

    cout << ret << "\n";

    return 0;
}
```
