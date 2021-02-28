## 음료수 얼려먹기(DFS/BFS)

```
from collections import deque


count=0
n, m=map(int,input().split())

graph=[]

for i in range(n):
    graph.append(list(map(int,input())))

def dfs(x,y):
    if x<0 or x>=n or y<0 or y>=m:
        return False
    if graph[x][y]==0:
        graph[x][y]=1
        dfs(x,y-1)
        dfs(x,y+1)
        dfs(x+1,y)
        dfs(x-1,y)
        return True
    return False

for i in range(n):
    for j in range(m):
        if dfs(i,j)==True:
            count+=1

print(count)
```

___

사용언어:python

문제출처: 이것이 취업을 위한 코딩테스트다