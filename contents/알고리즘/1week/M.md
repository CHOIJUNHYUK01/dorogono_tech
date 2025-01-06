[백준 3986](https://www.acmicpc.net/problem/3986)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, ret;
string s;
// 서로 교차되는 선이라면, 짝이 맞지 않는 경우임
stack<char> stk;

int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> s;

        // 홀수라면 무조건 불가능
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

        // 다음 문제를 위해 스택 초기화
        while (!stk.empty())
            stk.pop();
    }

    cout << ret << "\n";

    return 0;
}
```
