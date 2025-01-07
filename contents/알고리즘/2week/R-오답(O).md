[백준 1068](https://www.acmicpc.net/problem/1068)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, a[54], ret, r, d;
vector<int> adj[54];

int go(int here)
{
    int ret = 0;
    int child = 0;

    for (auto there : adj[here])
    {
        if (there == d)
            continue;
        // 각각 자식 값 다 더함
        ret += go(there);
        // 이게 있으면 자식이 있는 거니까
        child++;
    }

    // 없으면 끝이니까 자기 자신 1를 리턴
    if (child == 0)
        return 1;
    return ret;
}

int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> a[i];
        if (a[i] == -1)
        {
            r = i;
            continue;
        }
        adj[a[i]].push_back(i);
    }
    cin >> d;

    // 루트 노드를 지우면 없으니까 0 반환
    if (d == r)
    {
        cout << 0 << "\n";
        return 0;
    }

    cout << go(r) << "\n";

    return 0;
}
```
