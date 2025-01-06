[링크](https://www.acmicpc.net/problem/4949)

```
#include <bits/stdc++.h>
using namespace std;

string s;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    while (true)
    {
        getline(cin, s);

        if (s == ".")
            break;

        stack<char> stk;
        bool flag = false;

        for (int i = 0; i < s.size(); i++)
        {
            if (s[i] == '(' || s[i] == '[')
                stk.push(s[i]);
            else if (s[i] == ')')
            {
                if (stk.empty())
                {
                    flag = true;
                    break;
                }
                if (stk.top() == '(')
                    stk.pop();
                else
                    break;
            }
            else if (s[i] == ']')
            {
                if (stk.empty())
                {
                    flag = true;
                    break;
                }
                if (stk.top() == '[')
                    stk.pop();
                else
                    break;
            }
        }

        if (flag || stk.size())
            cout << "no" << "\n";
        else
            cout << "yes" << "\n";
    }

    return 0;
}
```
