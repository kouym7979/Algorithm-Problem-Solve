## 연산자 끼워넣기(DFS) 

```
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

int n;
vector<int> arr;

int add, sub, mul, divi;


int minValue = 1e9;
int maxValue = -1e9;


void dfs(int i, int now) {
    if (i == n) {
        minValue = min(minValue, now);
        maxValue = max(maxValue, now);
    }
    else {
        // 각 연산자에 대하여 재귀적으로 수행
        if (add > 0) {
            add -= 1;
            dfs(i + 1, now + arr[i]);
            add += 1;
        }
        if (sub > 0) {
            sub -= 1;
            dfs(i + 1, now - arr[i]);
            sub += 1;
        }
        if (mul > 0) {
            mul -= 1;
            dfs(i + 1, now * arr[i]);
            mul += 1;
        }
        if (divi > 0) {
            divi -= 1;
            dfs(i + 1, now / arr[i]);
            divi += 1;
        }
    }
}

int main(void) {
    cin >> n;
    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;
        arr.push_back(x);
    }
    cin >> add >> sub >> mul >> divi;

    // DFS 메서드 호출
    dfs(1, arr[0]);

    // 최댓값과 최솟값 차례대로 출력
    cout << maxValue << '\n' << minValue << '\n';
}
```

___

사용언어:c++

문제 출처: https://www.acmicpc.net/problem/14888