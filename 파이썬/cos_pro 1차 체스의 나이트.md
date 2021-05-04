## cos_pro 1차 체스의 나이트

```
from collections import deque


def solution(pos):
    answer = 0
    dx = [-1, -2, -2, -1, 1, 2, 2, 1]
    dy = [2, 1, -1, -2, -2, -1, 1, 2]

    map = [[0] * 8 for i in range(8)]
    visit = [[False] * 8 for i in range(8)]
    row = pos[0:1]

    row=int(ord(row)) - 65
    col = int(pos[1])

    visit[row][col] = True
    q = deque()
    q.append([row, col])

    while q:
        cx, cy = q.popleft()
        for i in range(8):
            nx = cx + dx[i]
            ny = cy + dy[i]
            if 0 <= nx < 8 and 0 <= ny < 8 and visit[nx][ny] == False:
                visit[nx][ny] = True
                answer += 1

    return answer


pos = "A7"
ret = solution(pos)
print(ret)
```

___

사용언어: python

문제출처: https://edu.goorm.io/learn/lecture/17299/cos-pro-1%EA%B8%89-%EA%B8%B0%EC%B6%9C%EB%AC%B8%EC%A0%9C-python/lesson/839016/1%EC%B0%A8-%EB%AC%B8%EC%A0%9C6-%EC%B2%B4%EC%8A%A4%EC%9D%98-%EB%82%98%EC%9D%B4%ED%8A%B8-python

