## 프로그래머스 level2 프린터

오늘은 프로그래머스의 level2문제인 프린터 문제를 풀어보았습니다.

이 문제는 큐와 우선순위큐를 적절히 이용하면 풀어내기 수월했던 문제였던 것 같습니다.

다음은 문제 설명입니다.

___

문제설명: 

```
1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.
```

예를 들어, 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다.

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다. 위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는 location이 매개변수로 주어질 때, 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.

다음은 코드입니다

___

```
#include <algorithm>
#include <cmath>
#include <iostream>
#include <vector>
#include <string>
#include <queue>


using namespace std;

int solution(vector<int> priorities, int location) {
	int answer = 0;
	queue<pair<int,int>> print;//현재 위치와 우선순위를 담음
	priority_queue<int> order;//우선순위를 담아줄 우선순위 큐
	
	
	for (int i = 0; i < priorities.size(); i++)
	{
		print.push(make_pair(i, priorities[i]));
		order.push(priorities[i]);
	}


	while (!print.empty())//
	{
		int x = print.front().first;//현재의 위치를 가져옴
		int y = print.front().second;//우선순위를 가져옴
		print.pop();

		if (y == order.top()) {//현재 제일 앞에있는 인쇄목록이 가장 우선순위가 높으면
			order.pop();
			answer++;

			if (x == location)//내가 인쇄를 요청한 문서면 끝
				break;
		}
		else//우선순위가 가장 높지 않으면
		{
			print.push(make_pair(x, y));//다시 맨뒤로 넣어줌
		}
	}
	
	return answer;
}

```

___

사용언어 : c++,c

출처: https://programmers.co.kr/learn/courses/30/lessons/42587