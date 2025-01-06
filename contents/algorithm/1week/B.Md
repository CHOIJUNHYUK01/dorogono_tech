[링크](https://www.acmicpc.net/problem/10808)

```
#include <bits/stdc++.h>
using namespace std;

string s;
int ret[30];

int main()
{
    cin >> s;

    for (auto c : s)
    {
        ret[c - 'a']++;
    }

    for (int i = 0; i < 26; i++)
    {
        cout << ret[i] << " ";
    }
    cout << "\n";

    return 0;
}
```
