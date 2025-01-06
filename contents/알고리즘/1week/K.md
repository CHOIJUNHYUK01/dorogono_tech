[링크](https://www.acmicpc.net/problem/1213)

```
#include <bits/stdc++.h>
using namespace std;

string s, ret;
int a[30], odd = -1;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> s;
    for (int i = 0; i < s.size(); i++)
    {
        a[s[i] - 'A']++;
    }

    for (int i = 25; i >= 0; i--)
    {
        if (a[i] % 2 == 1)
        {
            if (odd != -1)
            {
                cout << "I'm Sorry Hansoo" << "\n";
                exit(0);
            }
            odd = i;
            a[i] -= 1;
        }

        for (int j = 0; j < a[i]; j += 2)
        {
            ret = char(i + 'A') + ret + char(i + 'A');
        }
    }

    if (odd != -1)
    {
        int mid = ret.size() / 2;

        string prevRet = ret.substr(0, mid);
        string postRet = ret.substr(mid);

        cout << prevRet + char(odd + 'A') + postRet << "\n";
    }
    else
    {
        cout << ret << "\n";
    }

    return 0;
}
```
