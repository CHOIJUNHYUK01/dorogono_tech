[백준 1159](https://www.acmicpc.net/problem/1159)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

string s, ret = "";
int n, a[30]; // 성의 첫 글자 같아야 하니까 알파벳 저장

int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> s;
        a[s[0] - 'a']++;
    }

    for (int i = 0; i < 26; i++)
    {
        if (a[i] >= 5)
        {
            ret += char(i + 'a');
        }
    }

    if (ret.empty())
    {
        cout << "PREDAJA" << "\n";
    }
    else
    {
        cout << ret << "\n";
    }

    return 0;
}
```
