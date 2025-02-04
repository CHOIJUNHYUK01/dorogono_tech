[백준 9935](https://www.acmicpc.net/problem/9935)

<img src="https://skillicons.dev/icons?i=cpp" />

1. 문자열에서 폭발 문자열을 찾는 방법을 생각 <br />
2. str.find() 함수는 n \* m의 시간복잡도를 가짐 <br />
3. 최악의 상황일 때, 3천만이 나와서 폐기함 <br />
4. 대신 문자열을 O(n)을 가질 수 있도록 하나의 char를 추가하면서 확인하는 로직으로 변경

```cpp
#include <bits/stdc++.h>
using namespace std;

string s, b, ret;

int main()
{
    cin >> s >> b;

    for (char c : s)
    {
        ret += c;

        if (ret.size() >= b.size() && ret.back() == b[b.size() - 1])
        {
            string temp;
            for (int i = ret.size() - b.size(); i < ret.size(); i++)
            {
                temp += ret[i];
            }

            if (temp == b)
            {
                for (int j = 0; j < b.size(); j++)
                {
                    ret.pop_back();
                }
            }
        }
    }

    if (ret.size())
        cout << ret << "\n";
    else
        cout << "FRULA" << "\n";

    return 0;
}
```
