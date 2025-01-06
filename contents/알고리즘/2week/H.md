[링크](https://www.acmicpc.net/problem/4659)

```
#include <bits/stdc++.h>
using namespace std;

string s, tmp;
char cc[5] = {'a', 'e', 'i', 'o', 'u'};
bool pass = false;

bool checkIsMow(char c)
{
    for (int i = 0; i < 5; i++)
    {
        if (c == cc[i])
        {
            return true;
        }
    }
    return false;
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    while (cin >> s)
    {
        if (s == "end")
            break;

        // 1. 모음 확인
        pass = false;
        for (int i = 0; i < 5; i++)
        {
            if (s.find(cc[i]) != string::npos)
            {
                pass = true;
                break;
            }
        }

        if (!pass)
        {
            cout << '<' << s << '>' << " is not acceptable." << "\n";
            continue;
        }

        // 2. [ee, oo] 제외하고, 2개 연속 확인
        if (s.size() >= 2)
        {
            for (int i = 0; i < s.size() - 1; i++)
            {
                if (s[i] == s[i + 1])
                {
                    if (s[i] == 'e' || s[i] == 'o')
                        continue;

                    pass = false;
                    break;
                }
            }
        }

        if (!pass)
        {
            cout << '<' << s << '>' << " is not acceptable." << "\n";
            continue;
        }

        if (s.size() >= 3)
        {
            int mow = 0;
            int jao = 0;
            // 3. 3개 연속 확인
            for (int i = 0; i < s.size(); i++)
            {
                if (checkIsMow(s[i]))
                {
                    mow++;
                    jao = 0;
                    if (mow == 3)
                        break;
                }
                else
                {
                    mow = 0;
                    jao++;
                    if (jao == 3)
                        break;
                }
            }

            if (mow == 3 || jao == 3)
                pass = false;
        }

        if (!pass)
        {
            cout << '<' << s << '>' << " is not acceptable." << "\n";
            continue;
        }

        cout << '<' << s << '>' << " is acceptable." << "\n";
    }

    return 0;
}
```
