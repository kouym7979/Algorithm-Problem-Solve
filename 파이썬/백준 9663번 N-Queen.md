## 백준 9663번 N-Queen

## 문제

N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N이 주어진다. (1 ≤ N < 15)

## 출력

첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.

```
# 백트래킹
# DFS를 이용하여 백트래킹 알고리즘을 구현할 수 있다.
# 각 행을 차례대로 확인하면서, 각 열에 퀸을 놓는 경우를 고려한다.
# 이 때 위쪽 행을 모두 확인하며, 현재 위치에 놓을 수 있는지 확인해야한다.

def check(x):
    for i in range(x):
        if row[x] == row[i]:
            return False
        if abs(row[x] - row[i]) == x - i:
            return False
    return True


def dfs(x):
    global result
    if x == n:
        result += 1
    else:  # x번째 행의 각 열에 퀸을 둔다고 가정
        for i in range(n):
            row[x] = i
            if check(x):
                dfs(x + 1)


n = int(input())
row = [0] * n
result = 0
dfs(0)
print(result)
```

___

사용언어:python

문제출처: https://www.acmicpc.net/problem/9663