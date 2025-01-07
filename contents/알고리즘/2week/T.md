[백준 17298](https://www.acmicpc.net/problem/17298)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, a[1000004], ret[1000004];
stack<pair<int, int>> stk;

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> a[i];
    }

    for (int i = 0; i < n; i++)
    {
        // 비어있으면 자신이 기준이니, 스택에 넣기
        if (stk.empty())
        {
            stk.push({i, a[i]});
            continue;
        }

        // 지금 값이 스택에서 가장 큰 값보다 크다면,
        // 반환할 배열에 지금 값 넣고, 스택 pop
        while (stk.size() && a[i] > stk.top().second)
        {
            // 현재값보다 작은 애들 다 반환 배열에 값 넣어주기
            ret[stk.top().first] = a[i];
            stk.pop();
        }

        // 인덱스랑 현재 값 넣기
        // 인덱스 : 스택에서 본인보다 큰 값을 만나면
        // 반환 배열에 해당 인덱스에 값을 넣어줄 때 사용함
        stk.push({i, a[i]});
    }

    // 오큰수가 없다면, 스택이 차있음
    // 그 애들 전부 -1 대입
    while (stk.size())
    {
        int topIdx = stk.top().first;

        ret[topIdx] = -1;

        stk.pop();
    }

    for (int i = 0; i < n; i++)
    {
        cout << ret[i] << " ";
    }
    cout << "\n";

    return 0;
}
```
