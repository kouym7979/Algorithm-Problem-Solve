## N과 M(2) 백트래킹, 조합

## 문제

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

- 1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열
- 고른 수열은 오름차순이어야 한다.

## 입력

첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)

## 출력

한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.

수열은 사전 순으로 증가하는 순서로 출력해야 한다.

## 예제 입력 1 복사

```
3 1
```

## 예제 출력 1 복사

```
1
2
3
```

___

```
#include <algorithm>
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int n, m;//중복없이 m개를 고른 수열
//1~n개 까지의 자연수
int arr[9];
vector<int>sol;


int main()
{
	ios_base::sync_with_stdio(NULL);
	cin.tie(0);

	cin >> n >> m;

	for (int i = 1; i <= n; i++)
	{
		sol.push_back(i);
	}
	
	vector<int>idx(m,0);
	
	for (int i = 0; i < n - m; i++)
		idx.push_back(1);

	sort(idx.begin(), idx.end());

	do {
	
		for (int i = 0; i < idx.size(); i++)
		{
			if (idx[i] == 0)
				cout << sol[i]<<" ";
			
		}
		cout << endl;
	} while (next_permutation(idx.begin(), idx.end()));

	return 0;
}
```

문제설명: next_permutation을 이용한 조합 수열 출력

오름차순으로 출력하려면 idx벡터에서 0인값에 해당하는 sol[i]값을 출력하면 된다.

___

```
#include <algorithm>
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int n, m;//중복없이 m개를 고른 수열
//1~n개 까지의 자연수
int arr[9];
int sol[9];

void dfs(int c, int depth)
{
	if (depth == m)
	{
		for (int i = 0; i < m; i++)
		{
			cout << sol[i] << " ";
		}
		cout << endl;
		return;
	}

	for (int i =c; i < n; i++)
	{
		sol[depth] = arr[i]+1;
		dfs(i + 1, depth + 1);
	}

}

int main()
{
	ios_base::sync_with_stdio(NULL);
	cin.tie(0);

	cin >> n >> m;

	for (int i = 1; i <= n; i++)
	{
		arr[i]=i;
	}
	
	dfs(0, 0);


	
	return 0;
}
```

___

문제설명: dfs를 이용해서 반복횟수가 m개가 되면 수열을 출역하는 방식의 백트래킹을 구성했습니다.

사용언어:c++

문제출처:https://www.acmicpc.net/problem/15650