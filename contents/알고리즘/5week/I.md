[백준 3273](https://www.acmicpc.net/problem/3273)

<img src="https://skillicons.dev/icons?i=cpp" />

1. 중첩 for문은 불가능하다 판단 <br />
2. 가장 작은 수와 가장 큰 수를 기준으로 짝짓기 진행하기로 생각 <br />
3. 투 포인터를 활용해서 계산

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, a, x, l, r, ret;
vector<int> v;

int main()
{
    cin >> n;
    while (n--)
    {
        cin >> a;
        v.push_back(a);
    }
    cin >> x;
    sort(v.begin(), v.end());

    l = 0;
    r = v.size() - 1;

    while (l < r)
    {
        int sum = v[l] + v[r];

        if (sum < x)
        {
            l++;
        }
        else if (sum == x)
        {
            ret++;
            r--;
        }
        else
        {
            r--;
        }
    }

    cout << ret << "\n";

    return 0;
}
```
