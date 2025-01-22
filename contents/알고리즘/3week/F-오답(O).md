[링크](https://www.acmicpc.net/problem/16637)

<img src="https://skillicons.dev/icons?i=cpp" />

```cpp
#include <bits/stdc++.h>
using namespace std;

int n, ret = -987654321;
string s;
vector<int> v;
vector<char> op;

int calc(int a, int b, char sign)
{
    if (sign == '+')
        return a + b;
    else if (sign == '-')
        return a - b;
    else
        return a * b;
}

void go(int here, int val)
{
    // 인덱스가 끝까지 도달했을 경우, 끝냄
    if (here == v.size() - 1)
    {
        ret = max(ret, val);
        return;
    }

    // 기본 앞 순서대로 진행함
    go(here + 1, calc(val, v[here + 1], op[here]));

    // 만약에 다음 순서를 먼저 진행해도 되는지 확인함
    if (here + 2 <= v.size() - 1)
    {
        // 다음 계산식 먼저 진행
        int temp = calc(v[here + 1], v[here + 2], op[here + 1]);
        // 먼저 진행한 값과 현재 값 계산 진행
        go(here + 2, calc(val, temp, op[here]));
    }
}

int main()
{
    cin >> n >> s;
    for (char c : s)
    {
        if ('0' <= c && c <= '9')
            v.push_back(c - '0');
        else
            op.push_back(c);
    }

    go(0, v[0]);
    cout << ret << "\n";

    return 0;
}
```
