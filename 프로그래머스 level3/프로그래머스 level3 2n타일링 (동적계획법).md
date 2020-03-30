## 프로그래머스 level3 2*n타일링 (동적계획법)

###### 문제 설명

가로 길이가 2이고 세로의 길이가 1인 직사각형모양의 타일이 있습니다. 이 직사각형 타일을 이용하여 세로의 길이가 2이고 가로의 길이가 n인 바닥을 가득 채우려고 합니다. 타일을 채울 때는 다음과 같이 2가지 방법이 있습니다.

- 타일을 가로로 배치 하는 경우
- 타일을 세로로 배치 하는 경우

예를들어서 n이 7인 직사각형은 다음과 같이 채울 수 있습니다.

![Imgur](https://i.imgur.com/29ANX0f.png)

직사각형의 가로의 길이 n이 매개변수로 주어질 때, 이 직사각형을 채우는 방법의 수를 return 하는 solution 함수를 완성해주세요.

##### 제한사항

- 가로의 길이 n은 60,000이하의 자연수 입니다.
- 경우의 수가 많아 질 수 있으므로, 경우의 수를 1,000,000,007으로 나눈 나머지를 return해주세요.

------

##### 입출력 예

| n    | result |
| ---- | ------ |
| 4    | 5      |

##### 입출력 예 설명

입출력 예 #1
다음과 같이 5가지 방법이 있다.

![Imgur](https://i.imgur.com/keiKrD3.png)

![Imgur](https://i.imgur.com/O9GdTE0.png)

![Imgur](https://i.imgur.com/IZBmc6M.png)

![Imgur](https://i.imgur.com/29LWVzK.png)

![Imgur](https://i.imgur.com/z64JbNf.png)

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>


using namespace std;

int dp[60001];

int DP(int n )
{
	if (n == 1)
		return 1;
	if (n == 2)
		return 2;
	
	if (dp[n] != 0)
		return dp[n];
	return dp[n] = (DP(n - 1) + DP(n - 2))% 1000000007;
}

int solution(int n) {
	int answer = 0;

	answer=DP(n);

	return answer;
}
```

---

문제설명 : 가로의 길이가n인 사각형을 채우는 방법의 수를 구하는 문제입니다.

1. 먼저 만약 n=1이라면 주어진 타일을 세로로 세우는 방법밖에 없으므로 1을 리턴하고 n=2이라면 세로로 2개를 놓거나 가로로 2개를 놓는 방식으로 2가지입니다.

2. 즉 높이는 2로 고정이므로 가로의 길이 n을 만족하도록 점화식을 세우면 됩니다. 

3.  주어진 길이 n= n-2(가로로 놓았을 경우)+n-1(세로로 놓은 경우) 

   이런 점화식을 토대로 dp[n]=DP(n-1)+DP(n-2)를 넣어 점화식을 구현했습니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/12900