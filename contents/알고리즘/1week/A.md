[백준 2309](https://www.acmicpc.net/problem/2309)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

// 9명의 값이 들어옴
int a[9];

int main()
{
    for (int i = 0; i < 9; i++)
    {
        cin >> a[i];
    }
    // 순열을 돌 것이기에 오름차순으로 정렬
    sort(a, a + 9);

    do
    {
        next_permutation(a, a + 9);
    } while ((accumulate(a, a + 7, 0) != 100)); // 7명을 뽑을 것이기에 7명만 확인

    for (int i = 0; i < 7; i++)
    {
        cout << a[i] << "\n";
    }

    return 0;
}
```
