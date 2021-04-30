## Hacker Rank (Climbing the Leaderboard)

### 문제

An arcade game player wants to climb to the top of the leaderboard and track their ranking. The game uses [Dense Ranking](https://en.wikipedia.org/wiki/Ranking#Dense_ranking_.28.221223.22_ranking.29), so its leaderboard works like this:

- The player with the highest score is ranked number on the leaderboard.
- Players who have equal scores receive the same ranking number, and the next player(s) receive the immediately following ranking number.

**Example**



The ranked players will have ranks , , , and , respectively. If the player's scores are , and , their rankings after each game are , and . Return .

**Function Description**

Complete the climbingLeaderboard function in the editor below.

climbingLeaderboard has the following parameter(s):

- int ranked[n]: the leaderboard scores
- int player[m]: the player's scores

**Returns**

- int[m]: the player's rank after each new score

**Input Format**

The first line contains an integer , the number of players on the leaderboard.
The next line contains space-separated integers , the leaderboard scores in decreasing order.
The next line contains an integer, , the number games the player plays.
The last line contains space-separated integers , the game scores.



```
def climbingLeaderboard(ranked, player):
    result = []
    cnt = 0
    duplicate_rank = set(ranked)
    sub = list(duplicate_rank)
    sub = sorted(sub, reverse=True)

    for i in range(len(player)):
        for j in range(len(sub)):
            if player[i] >= sub[j]:
                result.append(j + 1)
                cnt += 1
                break
            elif player[i] < sub[-1]:
                result.append(len(sub) + 1)
                cnt += 1
                break
                
    return result
```

 다음과 같이 중복된 점수를 제거하기위해 set로 표현한 뒤 이중포문을 이용하여 구현을 해보았지만 테스트케이스의 run time error가 나와서 player의 점수가 오름차순으로 나타낸 점을 포인트로 인덱스를 통한 해결방법을 생각해보았다.

```
def climbingLeaderboard(ranked, player):
    cnt = 0
    duplicate_rank = set(ranked)
    sub = list(duplicate_rank)
    sub = sorted(sub, reverse=True)
    idx = len(sub)

    for i in player:
        while sub[idx - 1] <= i and idx > 0:
            idx -= 1
        if(idx<0):
            result.append(1)
            continue
        result.append(idx+1)
```

사용언어:python

문제출처: [www.hackerrank.com/challenges/climbing-the-leaderboard/problem](https://www.hackerrank.com/challenges/climbing-the-leaderboard/problem)