[백준 2559](https://www.acmicpc.net/problem/2559)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, k, temp, psum[100004], ret;

int main()
{
    cin >> n >> k;

    for (int i = 0; i < n; i++)
    {
        cin >> temp;

        // 첫 인덱스가 아닌 이상 계속해서 누적값을 넣어줄거임
        if (i != 0)
        {
            psum[i] = temp + psum[i - 1];
        }
        else
        {
            psum[i] = temp;
        }
    }

    // 첫 비교값 대입
    ret = psum[k - 1];

    for (int i = k; i < n; i++)
    {
        // 연속 날짜값만큼 값을 뽑아서 큰 값 뽑아내기
        ret = max(ret, psum[i] - psum[i - k]);
    }

    cout << ret << "\n";

    return 0;
}
```
