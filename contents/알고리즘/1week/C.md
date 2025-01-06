[백준 2979](https://www.acmicpc.net/problem/2979)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int a, b, c;
int t[104]; // 최대가 100임
int tin, tout;
int sum = 0;

int main()
{
    cin >> a >> b >> c;

    for (int i = 0; i < 3; i++)
    {
        cin >> tin >> tout;

        // 들어오고 한 틱 뒤부터 세거나, 들어오고 나가기 한 틱 전에 세어야 함
        for (int i = tin + 1; i <= tout; i++)
        {
            t[i]++; // 시간에 따라서 차 대수 확인
        }
    }

    for (int i = 1; i <= 100; i++)
    {
        if (t[i] == 1)
        {
            sum += a;
        }
        else if (t[i] == 2)
        {
            sum += b * 2;
        }
        else if (t[i] == 3)
        {
            sum += c * 3;
        }
    }

    cout << sum << "\n";

    return 0;
}
```
