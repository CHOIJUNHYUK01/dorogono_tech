[백준 1629](https://www.acmicpc.net/problem/1629)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int a, b, c;

int go(int n)
{
    if (n == 1)
        return a % c;

    // 계속 반으로 나누면서 진행
    long long ret = go(n / 2);

    // 값을 받으면 해당 값을 한 번 더 곱해야 함
    // 2제곱을 1제곱 값으로 받았으니까
    ret = (ret * ret) % c;

    // 버림으로 진행하기에 홀수라면, a를 곱해서 나머지 계산 추가로 함
    if (n % 2)
        ret = (ret * a) % c;

    return ret;
}

int main()
{
    cin >> a >> b >> c;

    // 그냥 제곱으로 하면 범위가 넘음
    // 제곱 수를 쪼개면서 진행하기로 생각함
    cout << go(b) << "\n";

    return 0;
}
```
