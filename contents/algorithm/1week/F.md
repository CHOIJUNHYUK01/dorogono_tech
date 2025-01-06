[링크](https://www.acmicpc.net/problem/11655)

```
#include <bits/stdc++.h>
using namespace std;

string s, ret;

int main()
{
    getline(cin, s);

    for (int i = 0; i < s.size(); i++)
    {
        if (!('a' <= s[i] && s[i] <= 'z') && !('A' <= s[i] && s[i] <= 'Z'))
        {
            ret += s[i];
        }
        else
        {
            if ('a' <= s[i] && s[i] <= 'z')
            {
                if (s[i] + 13 <= 'z')
                {
                    ret += char(s[i] + 13);
                }
                else
                {
                    ret += char(s[i] - 13);
                }
            }
            else
            {
                if (s[i] + 13 <= 'Z')
                {
                    ret += char(s[i] + 13);
                }
                else
                {
                    ret += char(s[i] - 13);
                }
            }
        }
    }

    cout << ret << "\n";

    return 0;
}
```
