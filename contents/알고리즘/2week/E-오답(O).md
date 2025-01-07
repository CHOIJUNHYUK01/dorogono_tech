[백준 1992](https://www.acmicpc.net/problem/1992)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n;
string s;
char a[68][68];

string go(int y, int x, int size)
{
    if (size == 1)
        return string(1, a[y][x]);

    // 처음 주어진 값을 기준으로 비교 시작함
    char std = a[y][x];
    string ret = "";
    for (int i = y; i < y + size; i++)
    {
        for (int j = x; j < x + size; j++)
        {
            // 하나라도 다르면 쪼개야 함
            if (a[i][j] != std)
            {
                ret += '(';
                ret += go(y, x, size / 2); // 좌상단
                ret += go(y, x + size / 2, size / 2); // 우상단
                ret += go(y + size / 2, x, size / 2); // 좌하단
                ret += go(y + size / 2, x + size / 2, size / 2); // 우하단
                ret += ')';

                return ret;
            }
        }
    }

    return string(1, std);
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> s;
        for (int j = 0; j < n; j++)
        {
            a[i][j] = s[j];
        }
    }

    cout << go(0, 0, n) << "\n";

    return 0;
}
```
