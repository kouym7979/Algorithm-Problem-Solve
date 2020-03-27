## 프로그래머스 level2-기능개발

오늘은 프로그래머스의 코딩문제를 풀어보았습니다. 스택과 큐에 관한 문제로 나와있었지만, 그냥 벡터로 풀었습니다.

___

문제 설명: 프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

제한 사항 및 입출력 예시는 출처를 통해 확인해 주세요.

___

```
#include <algorithm>
#include <cmath>
#include <iostream>
#include <vector>
#include <string>
#include <queue>

int m;
using namespace std;

vector<int> solution(vector<int> progresses, vector<int> speeds) {
	vector<int> answer;
	vector<int> complete;//작업진행의 갯수만큼 대입
	int count = 0;
	
	for (int i = 0; i < progresses.size(); i++)
	{
		m = (100 - progresses[i]) % speeds[i];//남은 진행 현황 
		if (m > 0)
		{
			complete.push_back((100-progresses[i])/ speeds[i]+1);//잔여일이 남아서 하루 더 해야하는지
		}
		else
		{
			complete.push_back((100 - progresses[i]) / speeds[i]);
		}
	}
	m = complete[0];//첫번째 기준
	for (int i = 0; i < complete.size(); i++)
	{
		if (m < complete[i]) {
			answer.push_back(count);
			count=1;
			m = complete[i];
		}
		else {
			count++;
		}
		if (i == complete.size() - 1)
		{
			answer.push_back(count);
		}
	}
	return answer;
}

```

___

이 문제는 잔여일을 비교하는 로직만 잘 생각하면 접근하기 쉬웠던 문제였던것 같습니다. 

조만간 큐를 이용한 풀이도 올리도록 하겠습니다.

사용언어: c++/c

출처:https://programmers.co.kr/learn/courses/30/lessons/42586