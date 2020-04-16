## 백준 1260번 DFS와 BFS

## 문제

그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

## 입력

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

## 출력

첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.

## 예제 입력 1 복사

```
4 5 1
1 2
1 3
1 4
2 4
3 4
```

## 예제 출력 1 복사

```
1 2 4 3
1 2 3 4
```

## 예제 입력 2 복사

```
5 5 3
5 4
5 2
1 2
3 4
3 1
```

## 예제 출력 2 복사

```
3 1 2 5 4
3 1 4 2 5
```

## 예제 입력 3 복사

```
1000 1 1000
999 1000
```

## 예제 출력 3 복사

```
1000 999
1000 999
```

___

```
#include <algorithm>
#include <iostream>
#include <vector>
#include <map>
#include <queue>

using namespace std;

vector<int>graph[10001];
vector<bool>visit(1001, false);
vector<bool>b_visit(1001, false);
void DFS(int s)
{
	visit[s] = true;
	cout << s;
	for (int i = 0; i < graph[s].size(); i++)
	{
		int next = graph[s][i];
		if (visit[next] != true)
			DFS(next);
	}

}


void BFS(int s,queue<int> q)
{
	b_visit[s] = true;
	q.push(s);

	while (!q.empty())
	{
		int next = q.front();
		q.pop();
		cout << next;
		for (int i = 0; i < graph[next].size(); i++)
		{
			if (b_visit[graph[next][i]] == false)
			{
				q.push(graph[next][i]);
				b_visit[graph[next][i]] = true;
			}
		}
	}
	
}

//여러개 이동가능한경우 정점 번호가 낮은것을 먼저 방문
int main()
{
	int n, m, v;//정점의 개수, 간선의 개수, 시작할 정점의 번호
	int start, end;
	queue<int>q;
	scanf("%d%d%d", &n, &m, &v);
	
	for (int i = 0; i < m; i++)//그래프 생성
	{
		scanf("%d%d",&start,&end);
		graph[start].push_back(end);
		graph[end].push_back(start);
	}

	for (int i = 0; i < n; i++)
	{
		sort(graph[i].begin(), graph[i].end());//연결된 것중에 점의 위치가 더 낮은것으로 이동하기위해서
	}

	DFS(v);
	cout <<endl;
	BFS(v,q);
	
	return 0;
}
```

____

문제설명: 

1. 간선의 정보에 따라서 정점을 연결하는 그래프를 만듭니다.
2. 문제의 조건중에 연결된 정점들중 여러개가 연결되있을 경우 숫자가 작은 정점부터 방문하기위해서 각 정점별로 오름차순으로 정렬을 합니다.
3. 각각 DFS와 BFS를 visit로 방문여부를 판단하여서 진행합니다.



사용언어:c++

출처:https://www.acmicpc.net/problem/1260