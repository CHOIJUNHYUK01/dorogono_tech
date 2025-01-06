[링크](https://www.acmicpc.net/problem/15353)

```
#include <bits/stdc++.h>
using namespace std;

string a, b, ret;

void go(string ra, string rb)
{
    int std = 0;
    int up = 0;
    int end = 0;
    bool endA = 0;

    if (ra.size() >= rb.size())
    {
        std = rb.size();
        end = ra.size();
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
    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());

    go(a, b);

    reverse(ret.begin(), ret.end());

    cout << ret << "\n";

    return 0;
}
```
