## 다익스트라 알고리즘 정리(feat. 최단경로)

그래프에서 정점끼리의 최단 경로를 구하는 문제는 여러가지 있습니다.

1. 하나의 정점에서 다른 하나의 정점까지의 최단 경로를 구하는 문제
2. 하나의 정점에서 다른 모든 정점까지의 최단 경로를 구하는 문제
3. 하나의 목적지로가는 모든 최단 경로를 구하는 문제
4. 마지막으로 모든 최단 경로를 구하는 문제

다익스트라 알고리즘은 여기서 2번째 방법에 해당합니다.(간선들은 모두 양의 간선들을 가져야한다)



다익스트라 알고리즘의 기본 로직은 첫 정점을 기준으로 연결되어있는 정점들을 추가해가며, 최단 거리를 갱신하는 것입니다.

정점을 잇기 전까지는 시작점을 제외한 정점들은 모두 무한대 값을 가집니다.

### **다익스트라 알고리즘(우선순위 큐)**

우선순위 큐를 이용하면 시간복잡도를 현저히 줄일 수가 있습니다.

![img](https://t1.daumcdn.net/cfile/tistory/271E224F5831E93B07)

1.  우선순위 큐를 이용할때 기본적으로 가장 큰 원소가 pop의 우선순위를 가지기 때문에 

가중치가 3,2,1이라는 값이 들어왔다면 우선순위는 3,2,1이 아닌 1,2,3이어야 하므로 음의 가중치로 바꾸어 우선순위큐에 넣습니다.

2.  A정점에서 B정점으로 가는 값이 이미 있는데 더 작은값이 생긴다면 우선순위큐에서 찾지 않고, 그냥 push한 후에, 나중에 가중치를 비교하여 가중치가 더 큰 것이었다면 무시하도록 합니다



우선순위 큐를 활용한 다익스트라 함수 코드입니다.

```
#include <iostream>
#include <vector>
#include <queue>
#include <limits.h>
#include <cstdio>
 
#define MAX_V 20001
 
using namespace std;
 
// 그래프의 인접 리스트. (연결된 정점 번호, 간선 가중치) 쌍을 담아야 한다.
vector< pair<int, int>> adj[MAX_V]; // 정점의 최대 개수 :: MAX_V
 
vector<int> dijkstra(int src, int V, int E)
{
    // V만큼 배열을 INT_MAX로 초기화
    vector<int> dist(V, INT_MAX);
    dist[src] = 0; // 시작점은 0으로 초기화 한다. 
 
    priority_queue<pair<int, int> > pq;
 
    pq.push(make_pair(0, src)); // 시작점을 처음으로 우선순위 큐에 삽입
 
    while (!pq.empty())
    {
        // 우선순위 큐에 음의 가중치로 들어가 있으니 양으로 바꾸어준다.
        int cost = -pq.top().first; 
        int here = pq.top().second;
 
        pq.pop();
 
        // 만약 지금 꺼낸 것보다 더 짧은 경로를 알고 있다면 지금 꺼낸것을 무시한다.
        if (dist[here] < cost)
            continue;
 
        // 인접한 정점들을 모두 검사.
        for (int i = 0; i < adj[here].size(); i++)
        {
            int there = adj[here][i].first;
            int nextDist = cost + adj[here][i].second;
 
            // 더 짧은 경로를 발견하면, dist[]를 갱신하고 우선순위 큐에 넣는다.
            // dist 벡터에는 시작점 -> there 위치까지의 최단 거리가 담겨있다.
            if (dist[there] > nextDist)
            {
                dist[there] = nextDist;
                pq.push(make_pair(-nextDist, there));
                /*
                여기서 -로 넣는 이유?
                priority_queue STL은 기본적으로 가장 큰 원소가 위로 가도록 큐를 구성
                따라서 거리의 부호를 바꿔서 거리가 작은 정점부터 꺼내지도록 하기 위함
                */
            }
        }
    }
 
    return dist;
}


출처: https://www.crocus.co.kr/546 [Crocus]
```

