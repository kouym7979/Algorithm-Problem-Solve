## NHN Pre-Test 1차 기출문제

#### 문제

 모든 원소가 0 또는 1 인 행렬이 있습니다. 1 로 표시된 원소는 영역을 나타냅니다. 여기에서 상하좌우에 인접한 1 은 같은 영역이라고 가정합니다. 각 영역의 크기는 1 의 개수로 정의합니다. 주어진 N x N 크기의 행렬에서 영역의 개수와 각 영역의 크기를 오름차순으로 출력하세요.

#### [입력] 

 • 첫 번째 행은 행렬의 크기인 N입니다. N 은 1 이상 10 이하의 자연수입니다.

 • 입력 두 번째 행부터는 공백으로 구분된 0 과 1 로 행렬이 주어집니다. 각 행은 개행 문자(newline, \n)로 구분됩니다.

#### [출력] 

• 첫 번째 행은 영역의 개수를 출력합니다.

• 두 번째 행은 각 영역의 크기를 공백으로 구분하여 오름차순으로 출력합니다. 

• 한 행의 끝은 불필요한 공백 없이 개행 문자(newline, \n)로 끝나야 합니다. 

• 영역이 존재하지 않을 경우 영역 수 0으로 1 행으로만 출력합니다.

___

```
#include <iostream>
#include <string>
#include <algorithm>
#include <vector>
#include <queue>


using namespace std;
int dx[] = { 1,-1,0,0 };
int dy[] = { 0,0,1,-1 };

int n;
int graph[11][11];
int visit[11][11] = {false,};
int cnt = 0;
void dfs(int x, int y)
{

	visit[x][y] = true;

	for (int i = 0; i < 4; i++)
	{
		int nx = x + dx[i];
		int ny = y + dy[i];

		if (nx < 0 || ny < 0 || nx >= n || ny >= n || graph[nx][ny] == 0 || visit[nx][ny] == true)
			continue;//확인할 필요없음
		else
		{
			cnt++;
			dfs(nx, ny);
		}
	}

	return;
}

int main()
{
	int k;
	vector<int>answer;
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			cin >> k;
			graph[i][j] = k;
			
		}
	}


	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{

			cnt = 0;
			if (visit[i][j] == false && graph[i][j] == 1) {
				cnt++;
				dfs(i, j);
				answer.push_back(cnt);
			}
		}
	}

	sort(answer.begin(), answer.end());
	if (answer.size() == 0)
		cout << "0";
	else {
		for (int i = 0; i < answer.size(); i++)
			cout << answer[i] << " ";
	}
	return 0;
}
```

___

사용언어:c++

문제출처: recruit.nhn.com

