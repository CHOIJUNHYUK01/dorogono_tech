[백준 1940](https://www.acmicpc.net/problem/1940)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n, m, a[15004], ret;

int main()
{
    cin >> n >> m;
    for (int i = 0; i < n; i++)
    {
        cin >> a[i];
    }

    // 두 개만 있으면 되고, 15,000 * 15,000 = 2억 3천만 정도니까 이중 for문 선택함
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            if (a[i] + a[j] == m)
                ret++;
        }
    }

    cout << ret << "\n";

    return 0;
}
```

## 개선 코드

```
#include<bits/stdc++.h>
using namespace std;

int n, m, arr[15004], ret;
map<int, int> mp;

int main(){
    ios_base::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);

    cin >> n >> m;

    for(int i=0; i<n; i++) {
        int v;
        cin >> v;

        arr[i] = v;

        // 필요한 재료값을 키값으로 해서 map을 만듦
        mp[m - v] = v;
    }

    // 이건 O(n)의 시간복잡도를 가짐
    for(int i=0; i<15004; i++) {
        if(arr[i] != 0 && mp[arr[i]] != 0) {
            ret++;
        }
    }

    // 양쪽값을 다 하기에 2배임
    cout << ret / 2 << "\n";

    return 0;
}

```
