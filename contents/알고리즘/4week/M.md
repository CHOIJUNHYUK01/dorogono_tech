[링크](https://www.acmicpc.net/problem/15353)

<img src="https://skillicons.dev/icons?i=cpp" />

```cpp
#include <bits/stdc++.h>
using namespace std;

string a, b, ret;

void go(string ra, string rb)
{
    int std = 0; // 짧은 숫자 길이
    int up = 0; // 올림 수
    int end = 0; // 끝나는 숫자 길이
    bool endA = 0; // 어떤 게 더 긴지

    if (ra.size() >= rb.size())
    {
        // 짧은 걸 기준으로 순회
        std = rb.size();
        // 하지만 끝나는 건 더 긴 것이기에 정해줌
        end = ra.size();
        // a가 긴 것인지, b가 긴 것인지 확인
        endA = 1;
    }
    else
    {
        std = ra.size();
        end = rb.size();
    }

    for (int i = 0; i < std; i++)
    {
        int stdA = ra[i] - '0';
        int stdB = rb[i] - '0';
        int sum = stdA + stdB;

        if (sum + up >= 10)
        {
            ret += (sum + up - 10) + '0';
            up = 1;
        }
        else
        {
            ret += (sum + up) + '0';
            up = 0;
        }
    }

    for (int i = std; i < end; i++)
    {
        if (endA)
        {
            if ((ra[i] - '0') + up >= 10)
            {
                ret += ((ra[i] - '0') + up - 10) + '0';
                up = 1;
            }
            else
            {
                ret += ((ra[i] - '0') + up) + '0';
                up = 0;
            }
        }
        else
        {
            if ((rb[i] - '0') + up >= 10)
            {
                ret += ((rb[i] - '0') + up - 10) + '0';
                up = 1;
            }
            else
            {
                ret += ((rb[i] - '0') + up) + '0';
                up = 0;
            }
        }
    }

    if (up)
    {
        ret += '1';
    }
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> a >> b;
    // 1의 자리부터 더해줘야 함.
    // 그래야 올림을 했을 때 계산이 가능.
    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());

    go(a, b);

    // 뒤집은 결과가 나오니, 다시 뒤집음
    reverse(ret.begin(), ret.end());

    cout << ret << "\n";

    return 0;
}
```
