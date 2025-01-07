[백준 9012](https://www.acmicpc.net/problem/9012)

<img src="https://skillicons.dev/icons?i=cpp" />

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

        // 괄호를 닫기 위해선 짝을 찾아야 함
        // 그러기 위해선 순서대로 차곡차곡 쌓고, 조건이 맞으면 빼는 스택이 알맞음
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
