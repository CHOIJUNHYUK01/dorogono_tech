[백준 2870](https://www.acmicpc.net/problem/2870)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int n;
string s;
vector<string> v;

bool cmp(const string &a, const string &b)
{
    if (a.size() == b.size())
    {
        return a < b;
    }
    return a.size() < b.size();
}

int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> s;
        string tmp = "";

        for (int j = 0; j < s.size(); j++)
        {
            int cn = s[j] - '0';

            if (cn >= 0 && cn <= 9)
            {
                // 숫자인 경우에만 스트링값으로 추가함
                tmp += s[j];
            }
            else
            {
                if (tmp.size())
                {
                    while (true)
                    {
                        // 0 없애기 로직
                        if (tmp.size() && tmp.front() == '0')
                            tmp.erase(tmp.begin());
                        else
                            break;
                    }
                    if (tmp.empty())
                        tmp = "0";
                    v.push_back(tmp);
                }
                tmp = "";
            }
        }

        if (tmp.size())
        {
            while (true)
            {
                if (tmp.size() && tmp.front() == '0')
                    tmp.erase(tmp.begin());
                else
                    break;
            }
            if (tmp.empty())
                tmp = "0";
            v.push_back(tmp);
        }
    }

    sort(v.begin(), v.end(), cmp);
    for (auto it : v)
    {
        cout << it << "\n";
    }

    return 0;
}
```
