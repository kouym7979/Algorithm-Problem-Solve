## Cos-pro 전광판 문구 출력

문제

전광판은 14자의 문구를 출력한다.

문구는 1초에 왼쪽으로 한칸씩 움직인다. 문구 이외의 부분은 "_"으로 표시된다.

어플은 설정한 문구를 화면에 반복해 출력해준다

```
# -*- coding: utf-8 -*-
# UTF-8 encoding when using korean


# -*- coding: utf-8 -*-
# UTF-8 encoding when using korean

from collections import deque


def solution(phrases, second):
    answer = ''
    temp = "______________"

    q = deque()
    for i in range(14):
        q.append("_")

    cnt = 0
    check = False
    for i in range(second):
        q.popleft()
        cnt += 1
        if check == False:
            q.append(phrases[i % 14])
        else:
            q.append("_")
        if cnt%14==0:
            if check==True:
                check=False
            else:check=True

    solve = []
    while q:
        solve.append(q.popleft())
    answer = ''.join(solve)
    return answer


phrases = "happy_birthday"
second = 15
print(solution(phrases, second))
```

___

사용언어:python

문제출처: https://edu.goorm.io/learn/lecture/17299/cos-pro-1%EA%B8%89-%EA%B8%B0%EC%B6%9C%EB%AC%B8%EC%A0%9C-python/lesson/839035/3%EC%B0%A8-%EB%AC%B8%EC%A0%9C5-%EC%A0%84%EA%B4%91%ED%8C%90-%EB%AC%B8%EA%B5%AC-%EC%B6%9C%EB%A0%A5-python