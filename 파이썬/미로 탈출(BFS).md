## 미로 탈출(BFS)

문제: nXm 크기의 미로를 탈출해야한다. 현 위치는 (1,1)에 있으며 미로의 출구는 (n,m)이다.

괴물이 있는 부분은 0 있는 부분은 1로 표시되어 있다. 탈출하기 위해 움직여야하는 최소 칸의 개수를 구하여라

```
from collections import deque


n,m= map(int, input().split())

graph=[]
for i in range(n):
    graph.append(list(map(int,input())))

dx=[1,-1,0,0]
dy=[0,0,-1,1]


def bfs(x,y):
    q=deque()
    q.append((x,y))
    while q:
        x,y=q.popleft()

        for i in range(4):
            nx=x+dx[i]
            ny=y+dy[i]
            if nx<0 or nx>=n or ny<0 or ny>=m:
                continue
            if graph[nx][ny]==0:
                continue
            if graph[nx][ny]==1:
                graph[nx][ny]=graph[x][y]+1
                q.append((nx,ny))

    return graph[n-1][m-1]

print(bfs(0,0))
```

___

사용언어:python

문제 출처: 이것이 취업을 위한 코딩테스트다