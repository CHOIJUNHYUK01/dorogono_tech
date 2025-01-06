[링크](https://www.acmicpc.net/problem/1436)

```
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

int n, tmp;
ll ret;
string s;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    for (int i = 666;; i++)
    {
        s = to_string(i);

        if (s.find("666") != string::npos)
        {
            tmp++;
        }

        if (tmp == n)
        {
            ret = i;
            break;
        }
    }

    cout << ret << "\n";

    return 0;
}
```
