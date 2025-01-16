[링크](https://www.acmicpc.net/problem/1094)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, ret = 0, x = 64;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;

    while (n != 0)
    {
        // 목표 길이보다 짧을 때까지 반으로 쪼갬
        if (x > n)
        {
            x = x >> 1;
            continue;
        }

        // 짧으면, 목표 길이에서 지금 막대기 길이만큼 뺌
        n -= x;
        // 빼면 그 만큼의 막대를 이어붙인 것이기에 1을 더해줌
        ret++;
    }

    cout << ret << "\n";

    return 0;
}
```
