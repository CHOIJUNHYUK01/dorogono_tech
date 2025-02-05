[백준 1931](https://www.acmicpc.net/problem/1931)

<img src="https://skillicons.dev/icons?i=cpp" />

1. 걸리는 회의 시간을 기준으로 했을 때, 확인 배열이 너무 길기에 기각 <br />
2. 각 회의가 끝나는 시간을 기준으로 정렬 <br />
3. 끝나는 시간을 기준으로 연속되는 회의를 추가함

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, s, e, ret;
vector<pair<int, int>> v;

int main()
{
    cin >> n;
    while (n--)
    {
        cin >> s >> e;
        v.push_back({e, s});
    }

    sort(v.begin(), v.end());
    e = 0;
    for (auto it : v)
    {
        if (it.second < e)
            continue;

        e = it.first;
        ret++;
    }

    cout << ret << "\n";

    return 0;
}
```
