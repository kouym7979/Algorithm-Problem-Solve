## 프로그래머스 level2 타겟 넘버

문제설명: n개의 음이 아닌 정수가 있습니다. 이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

```
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

##### 입출력 예

| numbers         | target | return |
| --------------- | ------ | ------ |
| [1, 1, 1, 1, 1] | 3      | 5      |

___

```
#include <string>
#include <vector>

using namespace std;

//타겟 넘버문제

int answer = 0;
void n_sum_dfs(vector<int> numbers, int t,int n,int count)//숫자 배열과 타겟 넘버를 받는다
{
	
	if (count == numbers.size())
	{
		if (n== t)
			answer++;
		return;
	}

	n_sum_dfs(numbers, t, n + numbers[count], count + 1);
	n_sum_dfs(numbers, t, n - numbers[count], count + 1);
}
int solution(vector<int> numbers, int target) {
	
	n_sum_dfs(numbers, target, 0, 0);

	return answer;
}
```

이 문제는 기본적인 DFS관련 문제입니다.  DFS를 재귀의 형태로 구성을 해서 n의 합이 target과 같을 경우 answer값을 증가시키는 구조로 작성했습니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/43165