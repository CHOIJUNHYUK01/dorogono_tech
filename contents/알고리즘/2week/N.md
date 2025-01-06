[링크](https://www.acmicpc.net/problem/9012)

```
#include <bits/stdc++.h>
using namespace std;

int t;
string s;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> t;
    while (t--)
    {
        cin >> s;

        stack<char> stk;
        for (int i = 0; i < s.size(); i++)
        {
            if (stk.empty())
            {
                stk.push(s[i]);
                continue;
            }

            if (stk.top() == '(' && s[i] == ')')
            {
                stk.pop();
            }
            else
            {
                stk.push(s[i]);
            }
        }

        if (stk.size())
            cout << "NO" << "\n";
        else
            cout << "YES" << "\n";
    }

    return 0;
}
```
