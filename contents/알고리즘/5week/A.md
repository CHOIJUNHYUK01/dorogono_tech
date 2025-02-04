[백준 2109](https://www.acmicpc.net/problem/2109)

<img src="https://skillicons.dev/icons?i=cpp" />

1. 가격을 기준으로 내림차순 진행 <br />
2. 우선순위 큐로 정렬 <br />
3. 해야 하는 최대 날짜를 기준으로 visited 배열로 확인 <br />
4. 이미 있다면, 최소 기간인 1일이 될 때까지 하루씩 앞당기며 확인

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, p, d, visited[10004], ret;
priority_queue<pair<int, int>> pq;

int main()
{
    cin >> n;
    memset(visited, 1, sizeof(visited));
    while (n--)
    {
        cin >> p >> d;
        pq.push({p, d});
    }

    while (pq.size())
    {
        tie(p, d) = pq.top();
        pq.pop();

        while (visited[d] == 0)
        {
            if (d == 0)
                break;
            d--;
        }

        if (d == 0)
            continue;

        visited[d] = 0;
        ret += p;
    }

    cout << ret << "\n";

    return 0;
}
```
