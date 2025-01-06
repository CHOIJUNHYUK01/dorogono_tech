[링크](https://www.acmicpc.net/problem/9996)

```
#include <bits/stdc++.h>
using namespace std;

int n, d;
string s, f, b, tw, twf, twb;

int main()
{
    cin >> n >> s;
    for (int i = 0; i < s.size(); i++)
    {
        if (s[i] == '*')
        {
            d = i;
            break;
        }
        f += s[i];
    }

    for (int i = d + 1; i < s.size(); i++)
    {
        b += s[i];
    }

    int testS = f.size() + b.size();

    for (int i = 0; i < n; i++)
    {
        tw = "";
        twb = "";
        twf = "";

        cin >> tw;

        if (tw.size() < testS)
        {
            cout << "NE" << "\n";
            continue;
        }

        for (int j = 0; j < f.size(); j++)
        {
            twf += tw[j];
        }

        if (twf != f)
        {
            cout << "NE" << "\n";
            continue;
        }

        for (int j = tw.size() - b.size(); j < tw.size(); j++)
        {
            twb += tw[j];
        }

        if (twb != b)
        {
            cout << "NE" << "\n";
            continue;
        }

        cout << "DA" << "\n";
    }

    return 0;
}
```

## 개선된 코드 (더 짧은 코드)

```
#include <bits/stdc++.h>
using namespace std;

int n;
string s, temp, prevS, postS;

int main()
{
    cin >> n >> s;

    int p = s.find('*');
    prevS = s.substr(0, p);
    postS = s.substr(p + 1);

    for (int i = 0; i < n; i++)
    {
        cin >> temp;

        int midL = temp.size() - prevS.size() - postS.size();
        if (midL < 0)
        {
            cout << "NE" << "\n";
            continue;
        }

        if (prevS == temp.substr(0, prevS.size()) && postS == temp.substr(prevS.size() + midL))
        {
            cout << "DA" << "\n";
        }
        else
        {
            cout << "NE" << "\n";
        }
    }

    return 0;
}
```
