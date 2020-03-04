## 프로그래머스 level2 더 맵게

문제 설명: 매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

```
섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
```

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- scoville의 길이는 1 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.

##### 입출력 예

| scoville             | K    | return |
| -------------------- | ---- | ------ |
| [1, 2, 3, 9, 10, 12] | 7    | 2      |

##### 입출력 예 설명

1. 스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
   새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5
   가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]
2. 스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.
   새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13
   가진 음식의 스코빌 지수 = [13, 9, 10, 12]

모든 음식의 스코빌 지수가 7 이상이 되었고 이때 섞은 횟수는 2회입니다.

___

처음에 문제를 벡터와 정렬을 이용해서 쉽게 접근해서 풀었습니다.. 하지만 너무 단순하게 풀었는지 테스트 케이스는 통과하였지만 효율성테스트에서는 통과를 하지못했습니다...



벡터와 정렬을 활용해서 풀어본 코드입니다.

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
using namespace std;

int solution(vector<int> scoville, int K) {
	int answer = 0;
	int degree = 0;//섞은 음식의 스코빌 지수
	
	
	while (1)
	{
        //스코빌 지수를 낮은 지수부터 높은 지수 순으로 나열
		sort(scoville.begin(), scoville.end());//기본적으로 오름차순 정리
        
		if (scoville.at(0) > K)//가장 작은값이 요구한 값보다 크면 종료
			break;
        if(scoville.size()==1 && scoville.at(0)<K)//만약 모든음식의 스코빌 지수를 k 이상으로 만들수 없는 경우
        {
            answer=-1;
            break;
        }

		degree = scoville.at(0) + (scoville.at(1) * 2);//섞은 스코빌 지수공식
		scoville.erase(scoville.begin());//섞은 음식 지수들 삭제
		scoville.erase(scoville.begin());
		scoville.push_back(degree);
		
		answer++;//섞은 횟수 증가
	}
	return answer;
}

```

위의 코드 결과 화면입니다.(그냥 참고용으로 봐주세요...)

![더맵게1](https://user-images.githubusercontent.com/52284829/75847968-1311f900-5e24-11ea-8f39-defc3646ffba.png)

다른 방식을 이용해서 풀어보았습니다. 우선순위 큐의 Max_heap을 이용해서 풀었습니다.

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
#include <queue>
using namespace std;

int solution(vector<int> scoville, int K) {
	int answer = 0;
	int degree = 0;//섞은 음식의 스코빌 지수
	int first, second;
	priority_queue<int, vector<int>, greater<int>> sco;//max_heap

	for (int i = 0; i < scoville.size(); i++)
	{
		sco.push(scoville[i]);//스코빌 지수들을 우선순위 큐에 넣어준다.
	}

	while (1)
	{
		if (sco.top() < K && sco.size()==1)
		{
			answer = -1;
			break;
		}
		
		else if (sco.top() > K) {
			break;
		}
		first = sco.top();
		sco.pop();
		second = sco.top();
		sco.pop();
		degree = first + second * 2;
		answer++;
		sco.push(degree);
	}

	

	return answer;
}

```

아슬아슬하게 효율성테스트도 통과한것 같습니다.![더맵게2](https://user-images.githubusercontent.com/52284829/75857316-5aef4b00-5e39-11ea-8aea-d1494cea2cc4.png)

___

이 문제를 풀고나서 효율성 부분에서 시간복잡도를 문제에 맞게 방향을 정해서 가는 것이 중요한것 같습니다. 다음 문제부터는 효율성부분도 염두해서 문제를 접근하도록 하겠습니다.