## 프로그래머스 level2 스킬트리

문제설명

선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

예를 들어 선행 스킬 순서가 `스파크 → 라이트닝 볼트 → 썬더`일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 `스파크 → 힐링 → 라이트닝 볼트 → 썬더`와 같은 스킬트리는 가능하지만, `썬더 → 스파크`나 `라이트닝 볼트 → 스파크 → 힐링 → 썬더`와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 skill과 유저들이 만든 스킬트리[1](https://programmers.co.kr/learn/courses/30/lessons/49993#fn1)를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

##### 제한 조건

- 스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.
- 스킬 순서와 스킬트리는 문자열로 표기합니다.
  - 예를 들어, `C → B → D` 라면 CBD로 표기합니다
- 선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.
- skill_trees는 길이 1 이상 20 이하인 배열입니다.
- skill_trees의 원소는 스킬을 나타내는 문자열입니다.
  - skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.

___

```
#include <algorithm>
#include <cmath>
#include <iostream>
#include <vector>
#include <string>
#include <queue>


using namespace std;

int solution(string skill, vector<string> skill_trees)
{
	int answer = 0;
	
	for (int i = 0; i < skill_trees.size(); i++)
	{
		vector<char> temp;//비교대상 저장

		for (int j = 0; j < skill_trees[i].size(); j++) {
			for (int k = 0; k < skill.size(); k++) {
				if (skill[k] == skill_trees[i][j]) {
					char tmp = skill[k];
					temp.push_back(tmp);//같은 문자일경우 푸쉬
				}
			}
		}
		bool flag = true;
		for (int x = 0; x < temp.size(); x++)
		{
			if (skill[x] != temp[x]) {
				flag = false;
			}
		}
		if (flag)
			answer++;
	}

	return answer;
}


```

이 문제는 3중포문을 이용해서 비교적 단순하게 접근해서 풀어보았습니다. 3중 포문으로 푼만큼 시간적인 부분에서는 비효율적이라고 생각이 되어서 다른 방식으로 풀어보도록 하겠습니다.