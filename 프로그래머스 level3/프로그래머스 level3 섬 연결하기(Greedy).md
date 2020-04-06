## 프로그래머스 level3 섬 연결하기(Greedy)

###### 문제 설명

n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.

다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.

**제한사항**

- 섬의 개수 n은 1 이상 100 이하입니다.
- costs의 길이는 `((n-1) * n) / 2`이하입니다.
- 임의의 i에 대해, costs[i][0] 와 costs[i] [1]에는 다리가 연결되는 두 섬의 번호가 들어있고, costs[i] [2]에는 이 두 섬을 연결하는 다리를 건설할 때 드는 비용입니다.
- 같은 연결은 두 번 주어지지 않습니다. 또한 순서가 바뀌더라도 같은 연결로 봅니다. 즉 0과 1 사이를 연결하는 비용이 주어졌을 때, 1과 0의 비용이 주어지지 않습니다.
- 모든 섬 사이의 다리 건설 비용이 주어지지 않습니다. 이 경우, 두 섬 사이의 건설이 불가능한 것으로 봅니다.
- 연결할 수 없는 섬은 주어지지 않습니다.

**입출력 예**

| n    | costs                                     | return |
| ---- | ----------------------------------------- | ------ |
| 4    | [[0,1,1],[0,2,2],[1,2,5],[1,3,1],[2,3,8]] | 4      |

**입출력 예 설명**

costs를 그림으로 표현하면 다음과 같으며, 이때 초록색 경로로 연결하는 것이 가장 적은 비용으로 모두를 통행할 수 있도록 만드는 방법입니다.

![image.png](https://grepp-programmers.s3.amazonaws.com/files/production/13e2952057/f2746a8c-527c-4451-9a73-42129911fe17.png)

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <queue>
#include <iostream>

using namespace std;

int land[101];//섬의 개수 최대 100개이므로

//Kruskal 알고리즘 
//그래프의 간선들을 가중치의 오름차순으로 정렬한다
//정렬된 간선 리스트에서 순서대로 사이클을 형성하지 않는 간선을 선택한다.
//사이클을 형성하는 간선을 제외한다.
//해당 간선을 MST(최소 비용 신장 트리)에 추가한다.

int island(int point)
{
	if (point == land[point])//자기 자신이면 리턴
		return point;
	else
		return island(land[point]);
}

bool cmp(const vector<int>&a, const vector<int>&b)//연결 비용 비교 
{
	return a[2] < b[2];
}

int solution(int n, vector<vector<int>> costs) {
	int answer = 0;
	int start = 0;
	int end = 0;
	int cost = 0;
	for (int i = 0; i < n; i++)
	{
		land[i] = i;//시작점 초기화
	}

	sort(costs.begin(), costs.end(), cmp);

	for (int i = 0; i < costs.size(); i++)
	{
		 start = island(costs[i][0]);//시작점
		 end = island(costs[i][1]);
		 cost = costs[i][2];

		 if (start != end)
		 {
			 land[start] = end;
			 answer+=cost;
		 }
	}


	return answer;
}
```

___

문제 설명: 이 문제는 Kruskal 알고리즘을 이용해서 풀이했습니다.

1.  먼저, 주어진 벡터의 간선들의 가중치를 오름차순으로 정렬하는 비교함수 cmp를 통해서 정렬합니다.

2. island함수를 통해서 각 지점의 시작점과 끝점을 넣고 재귀적으로 연결된 시작점을 찾습니다.

3. 연결이 되어 있으면 패스하고 시작점과 끝점이 다를 경우 그 경로의 가중치 값을 넣어줍니다.

   이 과정은 그래프의 싸이클이 형성되지 않도록 검사하는 것과 같다고 생각하시면 됩니다.



사용언어: c++

문제 출처: https://programmers.co.kr/learn/courses/30/lessons/42861