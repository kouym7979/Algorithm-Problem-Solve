## 프로그래머스 level3 이중우선순위큐

###### 문제 설명

이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.

| 명령어 | 수신 탑(높이)                  |
| ------ | ------------------------------ |
| I 숫자 | 큐에 주어진 숫자를 삽입합니다. |
| D 1    | 큐에서 최댓값을 삭제합니다.    |
| D -1   | 큐에서 최솟값을 삭제합니다.    |

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

##### 제한사항

- operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.
- operations의 원소는 큐가 수행할 연산을 나타냅니다.
  - 원소는 “명령어 데이터” 형식으로 주어집니다.- 최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.
- 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.

##### 입출력 예

| operations          | return |
| ------------------- | ------ |
| [I 16,D 1]          | [0,0]  |
| [I 7,I 5,I -5,D -1] | [7,5]  |

##### 입출력 예 설명

16을 삽입 후 최댓값을 삭제합니다. 비어있으므로 [0,0]을 반환합니다.
7,5,-5를 삽입 후 최솟값을 삭제합니다. 최대값 7, 최소값 5를 반환합니다.

___

```
#include <algorithm>
#include <vector>
#include <iostream>
#include <string>
#include <queue>

using namespace std;

// I 숫자 -> 큐에 주어진 숫자를 삽입합니다.
// D 1 -> 큐에서 최댓값을 삭제합니다.
// D -1 ->큐에서 최솟값을 삭제합니다.
//모든 연산 처리후에 큐가 비어있으면 [0,0]리턴 비어있지 않으면 [최대,최소]
vector<int> solution(vector<string> operations) {
	vector<int> answer;
	deque<int>sol;
	string temp;
	string sub;

	for (int i = 0; i < operations.size(); i++)
	{
		sub = operations.at(i);
		temp = "";
		for (int j = 2; j < operations[i].size(); j++)
		{
			temp += operations[i][j];
		}
		if (sub[0] == 'I')
		{
			sol.push_back(stoi(temp));
			sort(sol.begin(), sol.end());
		}
		else
		{
			if (sol.empty())//큐가 비어있으면 연산 무시 
			{
				continue;
			}
			if (stoi(temp) == 1)
			{
				sol.pop_back();
			}
			else //최솟값 삭제
			{
				sol.pop_front();
			}
		}
	}

	//모든연산을 처리한후
	if (sol.empty())
	{
		answer.push_back(0);
		answer.push_back(0);
	}
	else
	{
		answer.push_back(sol.back());
		answer.push_back(sol.front());
	}

	return answer;
}



```

___

문제설명:

1. 최대값과 최소값의 판별을 위해 탐색이 가능한 deque를 사용합니다
2. operation에 수행 연산과 수를 나누어서 저장하고 각 기능에 맞게 숫자를 넣거나 삭제를 합니다.
3. 모든 연산을 처리한후 조건에 맞게 answer에 넣어줍니다.



처음 벡터를 이용해서 풀었으나 이상하게.. temp==1부분에서 계속해서 core dump가 발생했습니다. 이유를 도저히 못 찾겠어서 deque를 이용해서 다시 풀어보았습니다.

(아직까지 모르겠습니다...)

사용언어:c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42628