[링크](https://www.acmicpc.net/problem/5430)

<img src="https://skillicons.dev/icons?i=cpp" />

```cpp
#include <bits/stdc++.h>
using namespace std;

int t, n;
string p, arr;

int main()
{
    cin >> t;
    while (t--)
    {
        cin >> p >> n >> arr;
        // reverse를 직접 할 수 없으니, 앞뒤로 뺄 수 있는 deque 선택
        deque<int> dq;

        // string으로 값이 들어오니, 각 숫자만 뽑아내야 함
        int x = 0;
        for (char c : arr)
        {
            if (c == '[' || c == ']')
                continue;

            if (c >= '0' && c <= '9')
                x = x * 10 + (c - '0');
            else
            {
                if (x > 0)
                    dq.push_back(x);

                x = 0;
            }
        }

        // 숫자 하나만 있다면 x값이 나올 수 있음
        if (x > 0)
            dq.push_back(x);

        bool r = false;
        bool flag = false;
        for (int i = 0; i < p.size(); i++)
        {
            if (p[i] == 'R')
            {
                r = !r;
            }
            else
            {
                // D일 경우에만 에러가 생길 수 있음
                if (dq.empty())
                {
                    flag = true;
                    break;
                }

                // 뒤집었을 때, 요소를 빼는 방향 조절
                if (r)
                    dq.pop_back();
                else
                    dq.pop_front();
            }
        }

        if (flag)
            cout << "error" << "\n";
        else
        {
            if (r)
                reverse(dq.begin(), dq.end());

            cout << "[";
            for (int i = 0; i < dq.size(); i++)
            {
                if (i == dq.size() - 1)
                {
                    cout << dq[i];
                    continue;
                }
                cout << dq[i] << ",";
            }
            cout << "]" << "\n";
        }
    }

    return 0;
}
```
