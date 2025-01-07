[백준 4949](https://www.acmicpc.net/problem/4949)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

string s;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    // 앞서 진행한 "괄호" 문제와 동일함
    // 다만 괄호의 종류가 많음
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
