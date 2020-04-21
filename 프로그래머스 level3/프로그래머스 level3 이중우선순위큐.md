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
	vector<int>sol;
	string temp = "";
	string sub;

	for (int i = 0; i < operations.size(); i++)
	{
		temp = "";
		sub = operations.at(0);
		if (sub[0] == 'I')
		{
			for (int j = 2; j < operations[i].size(); j++)//공백제외하고 숫자 부분만
			{
				temp += operations[i][j];
			}
			sol.push_back(stoi(temp));
		}
		else if (sub[0] == 'D')
		{
			if (sol.empty())//큐가 비어있으면 연산 무시 
			{
				continue;
			}
			else if (operations[i].at(2) == '1')
			{
				sort(sol.begin(), sol.end());
				sol.erase(sol.end());//최대값 삭제
			}
			else if (operations[i].at(2) == '-1')//최솟값 삭제
			{
				sort(sol.begin(), sol.end());
				sol.erase(sol.begin());
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

