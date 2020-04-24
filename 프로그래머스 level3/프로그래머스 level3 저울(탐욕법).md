## 프로그래머스 level3 저울(탐욕법)

###### 문제 설명

하나의 양팔 저울을 이용하여 물건의 무게를 측정하려고 합니다. 이 저울의 양팔의 끝에는 물건이나 추를 올려놓는 접시가 달려 있고, 양팔의 길이는 같습니다. 또한, 저울의 한쪽에는 저울추들만 놓을 수 있고, 다른 쪽에는 무게를 측정하려는 물건만 올려놓을 수 있습니다.

![image0.png](https://grepp-programmers.s3.amazonaws.com/files/production/f73e61d4de/f4abf5ff-1956-4e49-bd4a-d3d24619bbf0.png)

저울추가 담긴 배열 weight가 매개변수로 주어질 때, 이 추들로 측정할 수 없는 양의 정수 무게 중 최솟값을 return 하도록 solution 함수를 작성해주세요.

예를 들어, 무게가 각각 [3, 1, 6, 2, 7, 30, 1]인 7개의 저울추를 주어졌을 때, 이 추들로 측정할 수 없는 양의 정수 무게 중 최솟값은 21입니다.

##### 제한 사항

- 저울추의 개수는 1개 이상 10,000개 이하입니다.
- 각 추의 무게는 1 이상 1,000,000 이하입니다.

##### 입출력 예

| weight                 | return |
| ---------------------- | ------ |
| [3, 1, 6, 2, 7, 30, 1] | 21     |

##### 입출력 예 설명

문제에 나온 예와 같습니다.

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
#include <queue>

using namespace std;

int solution(vector<int> weight) {
	int answer = 0,sum=0;
	cin.tie(0);
	
	sort(weight.begin(), weight.end());//오름차순 정렬
	//1 1 2 3 6 7 30
	answer += weight[0];
	for (auto w : weight)
	{
		if (answer + 1 < w)
		{
			break;
		}
		else
			answer += w;
	}

	return answer;
}
```

___

문제설명: 

1. 주어진 무게들을 오름차순 정리합니다.
2. answer에 처음 무게값을 설정해주고 연속된 값이 나오지않는 무게의 값을 알아야하므로 answer+1이 다음 무게값보다 작을경우 그 값은 연속적으로 구할 수 없는 무게임을 파악합니다.
3. 그렇지 않을경우 다음 무게값을 늘려주면서 위의 과정을 반복합니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42886#qna