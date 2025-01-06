[링크](https://www.acmicpc.net/problem/2910)

```
#include <bits/stdc++.h>
using namespace std;

typedef pair<int, int> pp;

int n, c, tmp;
map<int, int> mp;    // 개수 저장
map<int, int> mpIdx; // 인덱스 저장

bool cmp(const pp &a, const pp &b)
{
    if (a.second == b.second)
    {
        return mpIdx[a.first] < mpIdx[b.first];
    }

    return a.second > b.second;
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> c;
    for (int i = 0; i < n; i++)
    {
        cin >> tmp;
        mp[tmp]++;
        if (mp[tmp] == 1)
            mpIdx[tmp] = i;
    }

    vector<pp> v(mp.begin(), mp.end());
    sort(v.begin(), v.end(), cmp);

    for (auto i : v)
    {
        for (int j = 0; j < i.second; j++)
        {
            cout << i.first << " ";
        }
    }
    cout << "\n";

    return 0;
}
```
