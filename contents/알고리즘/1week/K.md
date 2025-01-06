[백준 1213](https://www.acmicpc.net/problem/1213)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

string s, ret;
int a[30], odd = -1;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> s;
    for (int i = 0; i < s.size(); i++)
    {
        // 알파벳 개수 확인
        a[s[i] - 'A']++;
    }

    // 사전순 알파벳이니까 Z부터 붙이기 위해 역순으로 순회
    for (int i = 25; i >= 0; i--)
    {
        if (a[i] % 2 == 1)
        {
            // 홀수인 알파벳이 두 개라면 불가능
            if (odd != -1)
            {
                cout << "I'm Sorry Hansoo" << "\n";
                exit(0);
            }
            odd = i;
            a[i] -= 1;
        }

        for (int j = 0; j < a[i]; j += 2)
        {
            ret = char(i + 'A') + ret + char(i + 'A');
        }
    }

    // 홀수 알파벳이 있다면 그거 추가 로직
    if (odd != -1)
    {
        int mid = ret.size() / 2;

        string prevRet = ret.substr(0, mid);
        string postRet = ret.substr(mid);

        cout << prevRet + char(odd + 'A') + postRet << "\n";
    }
    else
    {
        cout << ret << "\n";
    }

    return 0;
}
```
