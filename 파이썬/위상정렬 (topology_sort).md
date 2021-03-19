## 위상정렬 (topology_sort)

```
#위상정렬
#위상정렬은 정렬 알고리즘의 일종이다. 위상 정렬은 순서가 정해져 있는 일련의 작업을 차례대로 수행해야 할 때 사용할 수 있는 알고리즘이다.
# 즉, 위상 정렬이란 방향그래프의 모든 노드를 '방향성에 거스르지 않도록 순서대로 나열하는 것'이다.
#1. 진입차수가 0인 노드를 큐에 넣는다.
#2. 큐가 빌 때까지 다음의 과정을 반복한다.
# ->큐에서 원소를 꺼내 해당노드에서 출발하는 간선을 그래프에서 제거한다.
# ->새롭게 진입차수가 0이된 노드를 큐에 넣는다.

from collections import deque

#노드의 개수와 간선의 개수를 입력받기
v,e=map(int,input().split())

indegree=[0]*(v+1) #각 노드에 대한 진입차수는 0으로 초기화
graph=[[] for _ in range(v+1)] #각 노드에 연결된 간선 정보를 담기 위한 연결 리스트 초기화

# 방향 그래프의 모든 간선 정보를 입력받기
for _ in range(e):
    a,b=map(int,input().split())
    graph[a].append(b)
    indegree[b]+=1 #진입차수 1증가

#위상 정렬함수
def topology_sort():
    result=[] #알고리즘 수행 결과를 담을 리스트
    q=deque() #큐 기능을 위한 deque 라이브러리 사용

    # 처음 시작할때는 진입차수가 0인 노드를 큐에 삽입
    for i in range(1,v+1):
        if indegree[i]==0:
            q.append(i)

    while q:
        now=q.popleft() #큐에서 원소 빼내기

        result.append(now)
        for i in graph[now]:
            indegree[i]-=1
            if indegree[i]==0:
                q.append(i)

    for i in result:
        print(i, end=' ')

topology_sort()
```

___

위상정렬의 시간복잡도는 O(V+E)이다.

위상정렬을 수행할 때는 차례대로 모든 노드를 확인하면서, 해당 노드에서 출발하는 간선을 차례대로 제거해야한다. 결과적으로 노드와 간선을 모두 확인한다는 측면에서 O(V+E)의 시간이 소요되는 것이다.