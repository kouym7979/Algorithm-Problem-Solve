## Cos-pro 비숍으로부터 도망쳐 -python

문제: 8X8크기의 체스판에서 주어진 비숍의 위치에서 이동할 수 있는 경로를 제외하고 남은 구역의 칸 개수를 출력하면된다.

```
from collections import deque


def solution(bishops):
    answer = 0

    dx = [-1, -1, 1, 1]
    dy = [1, -1, -1, 1]

    chess = [[False] * 9 for i in range(9)]
    cnt = 0
    for i in range(len(bishops)):
        row = int(ord(str(bishops[i])[0]) - 64)
        col = int(str(bishops[i])[1])
        if chess[row][col]==False:
            chess[row][col] = True
            cnt+=1
        print('시작점', row, col)
        q = deque()
        for i in range(4):
            q.append([row, col])
            while q:
                cx, cy = q.popleft()
                nx = cx + dx[i]
                ny = cy + dy[i]
                if 0 < nx <= 8 and 0 < ny <= 8:
                    if chess[nx][ny] == False:
                        chess[nx][ny] = True
                        print('처음', nx, ny)
                        cnt += 1
                        q.append([nx, ny])
                    else:
                        print('이미', nx, ny)
                        q.append([nx, ny])
    answer = 64 - cnt

    return answer

#bishop=["D5"]
bishop = ["D5", "E8", "G2"]

print(solution(bishop))
```



___

사용언어: python

문제출처: https://edu.goorm.io/learn/lecture/17299/cos-pro-1%EA%B8%89-%EA%B8%B0%EC%B6%9C%EB%AC%B8%EC%A0%9C-python/lesson/839033/3%EC%B0%A8-%EB%AC%B8%EC%A0%9C3-%EB%B9%84%EC%88%8D%EC%9C%BC%EB%A1%9C%EB%B6%80%ED%84%B0-%EB%8F%84%EB%A7%9D%EC%B3%90-python

