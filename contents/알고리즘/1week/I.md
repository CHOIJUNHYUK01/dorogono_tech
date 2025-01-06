[백준 1620](https://www.acmicpc.net/problem/1620)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

// 숫자 혹은 문자열로 들어올 것이기에 양쪽 다 만들어놓음
map<int, string> mp;
map<string, int> mp2;
int n, m;
string s, q;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        cin >> s;
        mp[i] = s;
        mp2[s] = i;
    }

    for (int i = 0; i < m; i++)
    {
        cin >> q;

        // 숫자인지 확인 (인덱스가 1부터니까 0이면 무조건 문자열임)
        if (atoi(q.c_str()) == 0)
        {
            cout << mp2[q] << "\n";
        }
        else
        {
            cout << mp[atoi(q.c_str())] << "\n";
        }
    }

    return 0;
}
```
