[백준 10988](https://www.acmicpc.net/problem/10988)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

string s;
int ret = 1;

int main()
{
    cin >> s;

    // index 절반만큼 순회하면서, 그에 맞는 짝 찾기
    for (int i = 0; i < s.size() / 2; i++)
    {
        // 맞지 않는 경우에만 ret을 0으로 바꿔주기
        if (s[i] != s[s.size() - i - 1])
        {
            ret = 0;
            break;
        }
    }

    cout << ret << "\n";

    return 0;
}
```
