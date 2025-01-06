[백준 10808](https://www.acmicpc.net/problem/10808)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

string s;
int ret[30];

int main()
{
    cin >> s;

    // 각 알파벳 순회
    for (auto c : s)
    {
        ret[c - 'a']++; // 0 ~ 25까지 값 추가
    }

    // 0:a, 1:b ... 25:z
    for (int i = 0; i < 26; i++)
    {
        cout << ret[i] << " ";
    }
    cout << "\n";

    return 0;
}
```
