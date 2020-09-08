## 미로 탈출(BFS)

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
#include <string>
#include <queue>

//미로탈출
//N*M 크기의 직사각형 형태의 미로
//현재 위치 (1,1) 미로의 출구는 (N,M)
//한번에 한칸씩 이동가능, 0: 괴물 ,1:괴물이 없는 곳
//탈출하기 위해 움직여야 하는 최소 칸의 개수를 구하시오 

//입력조건
// 4<=N,M<=200

using namespace std;

int maze[201][201];
int dx[] = { -1,1,0,0 };
int dy[] = { 0,0,-1,1 };


void BFS(int x, int y,int n,int m)
{
	queue<pair<int, int>>q;
	q.push(make_pair(x,y));

	while (!q.empty())
	{
		int cx = q.front().first;
		int cy = q.front().second;
		q.pop();
		for (int i = 0; i < 4; i++)
		{
			int nx = cx + dx[i];
			int ny = cy + dy[i];
		/*	cout << "\n";
			cout << nx << " " << ny<<"\n";
			cout << "n:" << n << " m:" << m << "\n";*/
			if (nx < 0 || ny < 0 || nx >= n || ny >= m)//벗어나면 안됨
			{
				continue;
			}
			if (maze[nx][ny] == 0)
				continue;//괴물이 있는곳
			
			if (maze[nx][ny] == 1)
			{
				maze[nx][ny] = maze[cx][cy] + 1;
				q.push(make_pair(nx,ny));
			}
		}
	}

	cout << maze[n - 1][m - 1];
	return;
}

int main()
{
	ios_base::sync_with_stdio(false);
	int n, m,answer=0;
	
	cin >> n >> m;

	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < m; j++)
		{
			scanf("%1d", &maze[i][j]);
		}
	}
	BFS(0, 0,n,m);

	

	return 0;
} 
```

___

사용언어:c++

문제출처: 이것이 취업을위한 코딩테스트다