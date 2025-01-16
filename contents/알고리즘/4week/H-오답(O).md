[링크](https://www.acmicpc.net/problem/11723)

<img src="https://skillicons.dev/icons?i=cpp" />

각 명령어를 조건문으로 풀어서 진행함. <br />
배열로 하면, `toggle`이나 `all`, `empty`을 할 때 순회를 하거나 조건문이 추가로 들어가기에 비트마스킹이 더 빠르다고 판단함. <br />
백준으로 한 결과, 시간 차이가 유의미하진 않았음.

### 비트마스킹

```cpp
#include <bits/stdc++.h>
using namespace std;

int m, n, x;
string s;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> m;
    while (m--)
    {
        cin >> s;
        if (s == "add")
        {
            cin >> x;
            n |= (1 << x);
        }
        else if (s == "remove")
        {
            cin >> x;
            n &= ~(1 << x);
        }
        else if (s == "check")
        {
            cin >> x;
            if (n & (1 << x))
            {
                cout << 1 << "\n";
            }
            else
            {
                cout << 0 << "\n";
            }
        }
        else if (s == "toggle")
        {
            cin >> x;
            n ^= (1 << x);
        }
        else if (s == "all")
        {
            n = (1 << 21) - 1;
        }
        else
        {
            n = 0;
        }
    }

    return 0;
}
```

### 배열

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, s[24];
string calc;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    while (n--)
    {
        cin >> calc;
        if (calc == "all")
        {
            for (int i = 1; i <= 20; i++)
            {
                s[i] = 1;
            }
        }
        else if (calc == "empty")
        {
            for (int i = 1; i <= 20; i++)
            {
                s[i] = 0;
            }
        }
        else
        {
            int temp;
            cin >> temp;

            if (calc == "add")
            {
                s[temp] = 1;
            }
            else if (calc == "check")
            {
                cout << s[temp] << "\n";
            }
            else if (calc == "remove")
            {
                s[temp] = 0;
            }
            else if (calc == "toggle")
            {
                if (s[temp])
                    s[temp] = 0;
                else
                    s[temp] = 1;
            }
        }
    }

    return 0;
}
```
