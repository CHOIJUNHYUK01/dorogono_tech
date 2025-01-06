[백준 11655](https://www.acmicpc.net/problem/11655)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

string s, ret;

int main()
{
    // 띄어쓰기 공백까지 받기
    getline(cin, s);

    for (int i = 0; i < s.size(); i++)
    {
        // 알파벳만 순회해야 하니까
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
                    // 26개라 최대범위 넘으면 -13으로 한 값과 동일함
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
