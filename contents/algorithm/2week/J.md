[링크](https://www.acmicpc.net/problem/10709)

```
#include <bits/stdc++.h>
using namespace std;

int h, w, a[104][104];
string s;

int main()
{
    cin >> h >> w;
    for (int i = 0; i < h; i++)
    {
        cin >> s;
        for (int j = 0; j < w; j++)
        {
            if (s[j] == 'c')
            {
                a[i][j] = 0;
            }
            else
            {
                a[i][j] = -1;
            }
        }
    }

    for (int i = 0; i < h; i++)
    {
        int start = -1;
        for (int j = 0; j < w; j++)
        {
            if (a[i][j] == 0)
            {
                start = j;
            }
            else
            {
                if (start != -1)
                {
                    a[i][j] = j - start;
                }
            }
        }
    }

    for (int i = 0; i < h; i++)
    {
        for (int j = 0; j < w; j++)
        {
            cout << a[i][j] << " ";
        }
        cout << "\n";
    }

    return 0;
}
```
