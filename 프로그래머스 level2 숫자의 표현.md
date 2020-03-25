## 프로그래머스 level2 숫자의 표현

###### 문제 설명

Finn은 요즘 수학공부에 빠져 있습니다. 수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다. 예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다.

- 1 + 2 + 3 + 4 + 5 = 15
- 4 + 5 + 6 = 15
- 7 + 8 = 15
- 15 = 15

자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return하는 solution를 완성해주세요.

##### 제한사항

- n은 10,000 이하의 자연수 입니다.

------

##### 입출력 예

| n    | result |
| ---- | ------ |
| 15   | 4      |

##### 입출력 예 설명

입출력 예#1
문제의 예시와 같습니다.

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>


using namespace std;

int answer = 0;//전체 가짓수
int BFS(int k,int i)//k가 찾아야할 값 i가 스타트할 값
{
	int sum = 0;
	while (sum <= k)
	{
		sum += i;
		i++;
		if (sum == k)
			answer++;
	}

	return 0;
}


int solution(int n) {
	
	for (int i = 1; i <= n; i++)
	{
		BFS(n, i);
	}

	return answer;
}
```

___

이번 문제는 정말 간단하게 해결이 가능한 문제인것 같습니다.

기본적인 조건인 연속적인 자연수의 합들로 주어진 자연수를 표현 가능한 가짓수를 문제이므로 1부터 주어진 자연수 까지 쭉 더해가면서 더한 값이 조건의 값과 같을 경우 answer값을 증가시켜주면 되는 문제입니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/12924 

