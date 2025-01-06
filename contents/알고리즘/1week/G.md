[백준 9996](https://www.acmicpc.net/problem/9996)

<img src="https://skillicons.dev/icons?i=cpp" />

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
        // * 위치 저장 (find로 찾기 가능)
        if (s[i] == '*')
        {
            d = i;
            break;
        }

        // 앞 글자 저장 (substr로 가능)
        f += s[i];
    }

    // 뒷 글자 저장 (substr로 가능)
    for (int i = d + 1; i < s.size(); i++)
    {
        b += s[i];
    }

    // 주어진 값 길이 확인용
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

        // 앞글자 확인
        for (int j = 0; j < f.size(); j++)
        {
            twf += tw[j];
        }

        if (twf != f)
        {
            cout << "NE" << "\n";
            continue;
        }

        // 뒷글자 확인
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
