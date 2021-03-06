## 프로그래머스 level3 예산

###### 문제 설명

국가의 역할 중 하나는 여러 지방의 예산요청을 심사하여 국가의 예산을 분배하는 것입니다. 국가예산의 총액은 미리 정해져 있어서 모든 예산요청을 배정해 주기는 어려울 수도 있습니다. 그래서 정해진 총액 이하에서 **가능한 한 최대의** 총 예산을 다음과 같은 방법으로 배정합니다.

```
1. 모든 요청이 배정될 수 있는 경우에는 요청한 금액을 그대로 배정합니다.
2. 모든 요청이 배정될 수 없는 경우에는 특정한 정수 상한액을 계산하여 그 이상인 예산요청에는 모두 상한액을 배정합니다. 
   상한액 이하의 예산요청에 대해서는 요청한 금액을 그대로 배정합니다. 
```

예를 들어, 전체 국가예산이 485이고 4개 지방의 예산요청이 각각 120, 110, 140, 150일 때, 상한액을 127로 잡으면 위의 요청들에 대해서 각각 120, 110, 127, 127을 배정하고 그 합이 484로 가능한 최대가 됩니다.
각 지방에서 요청하는 예산이 담긴 배열 budgets과 총 예산 M이 매개변수로 주어질 때, 위의 조건을 모두 만족하는 상한액을 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- 지방의 수는 3 이상 100,000 이하인 자연수입니다.
- 각 지방에서 요청하는 예산은 1 이상 100,000 이하인 자연수입니다.
- 총 예산은 `지방의 수` 이상 1,000,000,000 이하인 자연수입니다.

##### 입출력 예

| budgets              | M    | return |
| -------------------- | ---- | ------ |
| [120, 110, 140, 150] | 485  | 127    |

___

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> budgets, int M) {
	int answer = 0;
	long sum = 0;
	int check;
	int mid = 50000;
	int max = 100000;
	int min = 0;

	sort(budgets.begin(), budgets.end());

	for (int i = 0; i < budgets.size(); i++) {
		sum += budgets[i];
	}

	if (sum <= M)//전체 금액이 정부 예산보다 작으면 최대 금액이 상한가
		return *max_element(budgets.begin(),budgets.end());

	
	while (true) {
		sum = 0;
		for (int i = 0; i < budgets.size(); i++) {
			if (budgets[i] > mid) {//평균 이상보다 클경우 mid값을 더해줌 상한가 고려
				sum += mid;
			}
			else {
				sum += budgets[i];
			}
		}

		if (M < sum) {
			max = mid;
		}
		else if (M > sum) {
			min = mid;
		}
		else {
			return mid;
		}
		check = mid;
		mid = (min + max) / 2;

		if (mid == check) {
			return mid;
		}
	}

	return answer;
}

```

___

문제설명:

1. 주어진 지방의 예산 요청을 오름차순으로 정렬합니다.

2. 지방예산들의 합이 국가 예산보다 적으면 지방예산들의 최대값이 곧 상한가가 되므로 그 값을 반환해줍니다.

3. 2번의 경우가 아닌 경우 지방의 예산이 최소1원부터 100000이하의 수이므로 각 예산들이 중간값보다 클경우 중간값을 더해주고 작을 경우 그 예산을 그대로 더해 줍니다. 

4. 이렇게 더해준 총합이 국가예산보다 클경우 지방의 예산치의 최대값을 중간값으로 대체해주고 반대일 경우 최소값을 중간값으로 바꿔 줍니다. 그리고 다시 그 바뀐값을 토대로 중간값을 다시 산정합니다. 

   위의 과정을 반복하고 더이상 중간값이동이 없을경우 그 값을 반환합니다.



총 예산의 값을 고려하지못해 효율성에서 계속해서 잡아가지 못했습니다. 다음부턴 효율성을 고려해서 자료형 선언에 유의하도록 해야겠다는 생각을 했습니다...



사용언어:c++

출처:https://programmers.co.kr/learn/courses/30/lessons/43237#