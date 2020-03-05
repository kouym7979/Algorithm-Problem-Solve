## 프로그래머스 level2 주식가격

문제설명:

초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.

##### 제한사항

- prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
- prices의 길이는 2 이상 100,000 이하입니다.

##### 입출력 예

| prices          | return          |
| --------------- | --------------- |
| [1, 2, 3, 2, 3] | [4, 3, 1, 1, 0] |

##### 입출력 예 설명

- 1초 시점의 ₩1은 끝까지 가격이 떨어지지 않았습니다.
- 2초 시점의 ₩2은 끝까지 가격이 떨어지지 않았습니다.
- 3초 시점의 ₩3은 1초뒤에 가격이 떨어집니다. 따라서 1초간 가격이 떨어지지 않은 것으로 봅니다.
- 4초 시점의 ₩2은 1초간 가격이 떨어지지 않았습니다.
- 5초 시점의 ₩3은 0초간 가격이 떨어지지 않았습니다.

이 문제는 이해하는데에 시간이 오래걸렸습니다...

return 값을 주식의 값이 감소! 한 시점의 시간을 기록한다고 주어졌으면 좋았을것 같습니다.

___

처음은 벡터로 풀어보았으나... 몇개의 테스트 케이스를 통과하지 못했습니다.

```
#include <string>
#include <vector>
#include <queue>
using namespace std;
//queue는 탐색기능이 안되므로 deque를 사용하거나 stack을 이용하는 것이 좋음
//하지만 먼저 벡터를 이용해서 풀었습니다.
vector<int> solution(vector<int> prices) {
	vector<int> answer;
	
	for (int i = 0; i < prices.size(); i++)
	{
		int count = 0;
		
		if (i == prices.size() - 1)//마지막이면 0을 대입
		{
			answer.push_back(count);
			break;
		}
		for (int j = i + 1; j < prices.size(); j++)
		{
			if (prices[i] <= prices[j])//가격이 떨어지지 않았으면
			{
				count++;//유지된 기간 증가
			}
			else//가격이 떨어져도 기간은 증가시키고 정지
			{
				count++;
				break;
			}
		}
		answer.push_back(count);
	}

	return answer;
}
```

아래는 deque를 이용해서 풀이한 코드입니다.

```
#include <string>
#include <vector>
#include <queue>
#include <deque>
using namespace std;

vector<int> solution(vector<int> prices) {
	vector<int> answer;
	deque<int>dq;

	for (int i = 0; i < prices.size(); i++)
	{
		dq.push_back(prices[i]);
	}


	for (int i = 0; i < dq.size(); i++)
	{
		int temp = 0;
		int count = 0;
		temp = dq.at(i);
		if (i == dq.size() - 1)
		{
			answer.push_back(count);
			break;
		}
		for (int j = i + 1; j < dq.size(); j++)
		{
			if (temp <= dq[j])
			{
				count++;
			}
			else
			{
				count++;
				break;
			}
		}
		answer.push_back(count);
	}

	return answer;
}
```



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42584#qna