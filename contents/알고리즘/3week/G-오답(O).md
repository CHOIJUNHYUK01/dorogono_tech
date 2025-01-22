[링크](https://www.acmicpc.net/problem/12851)

<img src="https://skillicons.dev/icons?i=cpp" />

```cpp
#include <bits/stdc++.h>
using namespace std;

const int MAX = 200000;
int n, k, visited[MAX + 4], cnt[MAX + 4];

int main()
{
    cin >> n >> k;
    // 같은 위치라면 시간 0초, 방법은 1가지임
    if (n == k)
    {
        cout << 0 << "\n"
             << 1 << "\n";
        return 0;
    }

    // 움직일 수 있는 곳을 계산해야 하기에 qeueu를 선택함
    queue<int> q;
    q.push(n);
    visited[n] = 1;
    cnt[n] = 1;

    while (q.size())
    {
        int now = q.front();
        q.pop();

        // 움직일 수 있는 경로 확인
        for (int next : {now - 1, now + 1, now * 2})
        {
            if (next < 0 || next > MAX)
                continue;

            // 처음 방문한 곳 혹은 같은 시간에 도달한 곳만 확인함
            if (!visited[next])
            {
                // 한 번도 간 적이 없는 곳이라면, 시간을 더해줌
                visited[next] = visited[now] + 1;
                // 방법 수도 같이 더해줌
                cnt[next] += cnt[now];
                // 새로운 위치니, queue에 추가함
                q.push(next);
            }
            else if (visited[next] == visited[now] + 1)
            {
                // 같은 시간에 이미 방문한 곳이라면, 방법 수만 더해줌
                cnt[next] += cnt[now];
            }
        }
    }

    cout << visited[k] - 1 << "\n"
         << cnt[k] << "\n";

    return 0;
}
```
