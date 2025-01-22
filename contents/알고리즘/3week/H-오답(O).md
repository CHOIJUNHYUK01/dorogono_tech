[링크](https://www.acmicpc.net/problem/13913)

<img src="https://skillicons.dev/icons?i=cpp" />

```cpp
#include <bits/stdc++.h>
using namespace std;

#define prev aaa

const int MAX = 200000;
int n, k, visited[MAX + 4], prev[MAX + 4];

int main()
{
    cin >> n >> k;
    // 모든 이동 경로에 도착 시간을 위한 queue 사용
    queue<int> q;
    q.push(n);
    visited[n] = 1;

    while (q.size())
    {
        int now = q.front();
        q.pop();

        for (int next : {now - 1, now + 1, now * 2})
        {
            if (next < 0 || next > MAX || visited[next])
                continue;

            // 다음 경로 시간 계산
            visited[next] = visited[now] + 1;
            // 이전 위치 저장
            prev[next] = now;
            q.push(next);
        }
    }

    cout << visited[k] - 1 << "\n";

    vector<int> v;
    for (int i = k; i != n; i = prev[i])
        v.push_back(i);

    // 내 시작 위치는 이 값에 없으니 추가해줌
    v.push_back(n);
    reverse(v.begin(), v.end());

    for (auto it : v)
        cout << it << " ";
    cout << "\n";

    return 0;
}
```
