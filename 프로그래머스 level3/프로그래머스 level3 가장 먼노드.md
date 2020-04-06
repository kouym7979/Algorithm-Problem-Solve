## 프로그래머스 level3 가장 먼노드

###### 문제 설명

n개의 노드가 있는 그래프가 있습니다. 각 노드는 1부터 n까지 번호가 적혀있습니다. 1번 노드에서 가장 멀리 떨어진 노드의 갯수를 구하려고 합니다. 가장 멀리 떨어진 노드란 최단경로로 이동했을 때 간선의 개수가 가장 많은 노드들을 의미합니다.

노드의 개수 n, 간선에 대한 정보가 담긴 2차원 배열 vertex가 매개변수로 주어질 때, 1번 노드로부터 가장 멀리 떨어진 노드가 몇 개인지를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 노드의 개수 n은 2 이상 20,000 이하입니다.
- 간선은 양방향이며 총 1개 이상 50,000개 이하의 간선이 있습니다.
- vertex 배열 각 행 [a, b]는 a번 노드와 b번 노드 사이에 간선이 있다는 의미입니다.

##### 입출력 예

| n    | vertex                                                   | return |
| ---- | -------------------------------------------------------- | ------ |
| 6    | [[3, 6], [4, 3], [3, 2], [1, 3], [1, 2], [2, 4], [5, 2]] | 3      |

##### 입출력 예 설명

예제의 그래프를 표현하면 아래 그림과 같고, 1번 노드에서 가장 멀리 떨어진 노드는 4,5,6번 노드입니다.

![image.png](https://grepp-programmers.s3.amazonaws.com/files/ybm/fadbae38bb/dec85ab5-0273-47b3-ba73-fc0b5f6be28a.png)

___

```
#include <string>
#include <vector>
#include <queue>
#include <algorithm>
#include <iostream>
#include <list>

using namespace std;
//1번노드에서 가장 멀리 떨어진 노드가 몇 개인지 구하라

int solution(int n, vector<vector<int>> edge) {
	int answer = 0;
	vector<vector<int>>graph(n + 1, vector<int>());//그래프 생성
	vector<bool>visit(n + 1, false);//이동 판단여부
	vector<int>dis(n + 1, 0);//각 노드에서의 거리 0으로 초기화
	queue<int>q;

	for(int i=0;i<edge.size();i++)
	{
		graph[edge[i][0]].push_back(edge[i][1]);
		graph[edge[i][1]].push_back(edge[i][0]);
	}

	
	q.push(1);//시작점 
	dis[1] = 0;
	visit[1] = true;

	while (!q.empty())
	{
		int start = q.front();
		q.pop();
		for (int i = 0; i<graph[start].size(); i++)//시작점에서 연결된 곳이 있는만큼
		{
			if (visit[graph[start][i]] == false)//아직 방문하지 않은 곳이면
			{
				q.push(graph[start][i]);//다음 칸으로 이동
				visit[graph[start][i]] = true;//방문했으므로 true로 변경
				dis[graph[start][i]] =dis[start]+1;//방문한 지점은 전 지점에서의 거리값에1씩 더해서 갱신
			}
		}
	}

	int Max = *max_element(dis.begin(), dis.end());
	
	for (int i = 1; i <= n; i++)
	{
		if (dis[i] == Max)
		{
			answer++;
		}
	}
	return answer;
}
```

___

문제설명: 문제에서 주어진 노드에 따른 그래프를 그려준 후 그래프의 이동경로를 판단하여 출발점에서 이동한 점까지의 거리를 갱신해줍니다.

1. 2차원 벡터를 통해서 그래프의 점을 넣습니다.
2. 문제에서 시작점은 1로하므로 q에 시작점인 1을 넣고 그래프에서 시작점에 연결된 점으로 이동합니다. 이때 이동한점은 true로 변경해주고 다시 이동하지 않게 합니다.
3. 이동된 점을 시작점으로 바꿔주고 그 점에서 다시 연결된 점으로 이동합니다. 큐에 스타트 지점을 계속 푸시하며 큐가 다 팝될경우 종료합니다.



거리만 넣은 벡터에서 최대값을 구하여 그 최댓값과 같은 벡터의 index만큼 멀리 떨어진 점들이 가장 멀리 떨어진 노드입니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/49189