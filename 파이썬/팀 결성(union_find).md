## 팀 결성

```
import sys

#팀결성
# k가 0일경우에는 팀 합치기 연산을 진행한다.
# k가 1일경우에는 같은 팀 여부 확인을 한다.

def find_parent(parent,x): #같은 팀 여부확인
    if parent[x]!=x:
        parent[x]=find_parent(parent,parent[x])
    return parent[x]

def union_parent(parent,a,b):
    a=find_parent(parent,a)
    b=find_parent(parent,b)

    if a<b:
        parent[b]=a
    else: parent[a]=b

n,m=map(int,input().split())
parent=[0]*(n+1) #부모테이블 초기화

for i in range(1,n+1):
    parent[i]=i #부모테이블 자기 자신으로 초기화

for i in range(m):
    k,a,b=map(int,input().split())
    if k==0:
        union_parent(parent,a,b)
    elif k==1:
        x=find_parent(parent,a)
        y=find_parent(parent,b)
        if x==y:
            print('YES')
        else: print('NO')
```

___

사용언어: python

문제 출처: 이것이 취업을 위한 코딩테스트다