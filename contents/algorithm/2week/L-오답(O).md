[링크](https://www.acmicpc.net/problem/2852)

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

        if (g == 1)
            aScore++;
        else
            bScore++;

        if (win == 1)
            retA += stdT - prevT;
        else if (win == 2)
            retB += stdT - prevT;

        if (aScore > bScore)
            win = 1;
        else if (aScore == bScore)
            win = 0;
        else
            win = 2;

        prevT = stdT;
    }

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
