[링크](https://www.acmicpc.net/problem/3986)

```
#include <bits/stdc++.h>
using namespace std;

int n, ret;
string s;
stack<char> stk;

int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> s;

        if (s.size() % 2 == 1)
            continue;

        for (int i = 0; i < s.size(); i++)
        {
            if (!stk.empty())
            {
                if (stk.top() == s[i])
                    stk.pop();
                else
                    stk.push(s[i]);
            }
            else
            {
                stk.push(s[i]);
            }
        }

        if (stk.empty())
            ret++;

        while (!stk.empty())
            stk.pop();
    }

    cout << ret << "\n";

    return 0;
}
```
