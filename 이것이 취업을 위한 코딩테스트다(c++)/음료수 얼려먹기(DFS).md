## 음료수 얼려먹기(DFS)

##### 음료수 얼려먹기

N*M 크기의 얼음 틀이 있다. 구멍이 뚫려있는 부분은 0, 칸막이가 존재하는 부분은 1로 표시
구멍이 뚫려있는 부분끼리 상,하,좌,우로 붙어 있는 경우 서로 연결되어 있는 것으로 간주한다.
이때 얼음 틀의 모양이 주어졌을 때 생성되는 총 아이스크림의 개수를 구하는 프로그램을 작성하시오.

##### 입력조건

첫 번째 줄에 얼음 틀의 세로 길이 N과 가로길이 M이 주어진다 (1<=N,M<=1000)
두 번재 줄부터 N+1번째 줄까지 얼음 틀의 형태가 주어진다, 0:구멍, 1:구멍이 뚫리지않은곳
한 번에 만들 수 있는 아이스크림의 개수를 출력하라

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
#include <string>
#include <queue>

using namespace std;

int ice[1000][1000];//얼음틀

int n, m;

bool dfs(int x, int y)
{
	if (x<0 || y<0 || x>=n || y>=m)//얼음틀을 벗어난 경우 종료
		return false;

	if (ice[x][y] ==0)
	{
		ice[x][y] = 1;//방문처리
		dfs(x - 1, y);//상하좌우 판단
		dfs(x , y-1);
		dfs(x+1, y);
		dfs(x, y +1);
		return true;
	}

	return false;

}

int main()
{
	ios_base::sync_with_stdio(false);
	
	int answer = 0;
	cin >> n >> m;

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < m; j++)
		{
			scanf("%1d", &ice[i][j]);//띄어쓰기가 없이 숫자가 입력이 될경우 scanf의 %1d로 입력 받으면 숫자1개씩 입력이된다.
		}
	}
	
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < m; j++)
		{
			if(dfs(i, j)==true)
				answer++;
		}
	}

	cout << answer;

	return 0;
} 
```

___

문제 설명: 주어진 얼음틀에서 생성될 수 있는 얼음의 개수를 구하는 문제입니다.

이 문제를 해결하기 위해서 DFS방식을 이용하여 얼음틀에서 상,하,좌,우를 판단할 때 이미 채워진 공간을 만나는 횟수를 셈으로써 문제를 해결했습니다.



사용언어:c++

문제출처: 이것은 취업을 위한 코딩테스트다 

