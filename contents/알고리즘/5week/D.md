[백준 14469](https://www.acmicpc.net/problem/14469)

<img src="https://skillicons.dev/icons?i=cpp" />

1. 소가 들어오는 시간을 기준으로 정렬 <br />
2. 검문이 끝나는 시간 안에 소가 들어오면, 그 소는 대기 <br />
3. 대기 하는 소의 검문 시간을 끝나는 시간에 더해줌 <br />
4. 더하면, 그만큼 빈틈없이 시간을 소비할 수 있기에 더 효과적임 <br />
5. 끝나는 시간 이외라면, 시작 시간과 끝나는 시간을 그 소에 맞게 다시 조정하고 2-4번 반복

```cpp
#include <bits/stdc++.h>
using namespace std;

int l, r, n, inc, outc;
vector<pair<int, int>> v;

int main()
{
    cin >> n;
    while (n--)
    {
        cin >> inc >> outc;
        v.push_back({inc, outc});
    }

    sort(v.begin(), v.end());
    l = v[0].first;
    r = l + v[0].second;

    for (int i = 1; i < v.size(); i++)
    {
        if (v[i].first <= r)
        {
            r += v[i].second;
        }
        else
        {
            l = v[i].first;
            r = l + v[i].second;
        }
    }

    cout << r << "\n";

    return 0;
}
```
