## 프로그래머스 level2 H-index(정렬)

문제설명: H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과[1](https://programmers.co.kr/learn/courses/30/lessons/42747#fn1)에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 `n`편 중, `h`번 이상 인용된 논문이 `h`편 이상이고 나머지 논문이 h번 이하 인용되었다면 `h`가 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

##### 입출력 예

| citations       | return |
| --------------- | ------ |
| [3, 0, 6, 1, 5] | 3      |

##### 입출력 예 설명

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

___

```
#include <string>
#include <vector>
#include <cmath>
#include <algorithm>
using namespace std;

int solution(vector<int> citations) {
	int answer = 0;
	int count,n_count = 0;//count는 나머지 논문의 수 n_count는 몇번째 논문인지

	
	sort(citations.begin(), citations.end(),greater<int>());//내림차순으로 정리

	for (int i = 0; i < citations.size(); i++)
	{
		if (citations[i] <= answer)
			break;
		answer++;

	}
	return answer;
}


```

이번문제는 H-index에 대한 눈치가 빨랐다면 엄청 빠르게 풀 수 있었던 문제인 것 같습니다.

문제에서 요구한 H-index는 주어진 배열을 내림차순 정리 했을때 주어진 배열의 i값이 H-index값보다 작거나 같으면 인용된 논문의 수는 자동적으로 조건이 성립하게 됩니다. 



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42747