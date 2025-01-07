[백준 2852](https://www.acmicpc.net/problem/2852)

<img src="https://skillicons.dev/icons?i=cpp" />

```
#include <bits/stdc++.h>
using namespace std;

int wholeTime = 2880;
int n, g, retA, retB, prevT, aScore, bScore, win;
string s;

void getAnswer(int teamTime)
{
    string minS = to_string(teamTime / 60);
    string secS = to_string(teamTime % 60);

    if (minS.size() == 1)
        minS = '0' + minS;
    if (secS.size() == 1)
        secS = '0' + secS;

    cout << minS << ":" << secS << "\n";
}

int main()
{
    ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n;
    for (int i = 0; i < n; i++)
    {
        cin >> g >> s;

        int mm = stoi(s.substr(0, 2)) * 60;
        int ss = stoi(s.substr(3));
        int stdT = mm + ss;

        // 누적 골
        if (g == 1)
            aScore++;
        else
            bScore++;

        // 이전에 이기고 있는 팀에 따라 시간 계산
        // 현재 골이 들어간 시간에서 이전 골 들어간 시간을 뺌
        if (win == 1)
            retA += stdT - prevT;
        else if (win == 2)
            retB += stdT - prevT;

        // 현재 골 추가 후, 승패팀 결정
        if (aScore > bScore)
            win = 1;
        else if (aScore == bScore)
            win = 0;
        else
            win = 2;

        // 현재 주어진 시간을 이전 기준 시간으로 지정
        prevT = stdT;
    }

    // 이제 기준은 끝나는 시간이니까
    if (win == 1)
    {
        retA += wholeTime - prevT;
    }
    else if (win == 2)
    {
        retB += wholeTime - prevT;
    }

    getAnswer(retA);
    getAnswer(retB);

    return 0;
}
```
