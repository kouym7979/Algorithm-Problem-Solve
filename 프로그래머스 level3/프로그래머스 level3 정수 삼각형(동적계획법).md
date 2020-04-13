## 프로그래머스 level3 정수 삼각형(동적계획법)

###### 문제 설명

![스크린샷 2018-09-14 오후 5.44.19.png](https://grepp-programmers.s3.amazonaws.com/files/production/97ec02cc39/296a0863-a418-431d-9e8c-e57f7a9722ac.png)

위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

##### 제한사항

- 삼각형의 높이는 1 이상 500 이하입니다.
- 삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.

##### 입출력 예

| triangle                                                | result |
| ------------------------------------------------------- | ------ |
| [[7], [3, 8], [8, 1, 0], [2, 7, 4, 4], [4, 5, 2, 6, 5]] | 30     |

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;


//왼쪽과 오른쪽의 합의 경우에서 큰값으로 이동
int solution(vector<vector<int>> triangle) {
	int answer = 0;
	
	for (int i = 1; i < triangle.size(); i++)
	{// 깊이당 맥스값을 찾아서 그것을 기준으로 다시 왼쪽 오른쪽 계산
		for (int j = 0; j < triangle[i].size(); j++)
		{
			if (j == 0)
			{
				triangle[i][j] += triangle[i-1][j];//제일 왼쪽은 제일 왼쪽것만 비교

			}
			else if (j == i)//마지막 끝값일 경우 
			{
				triangle[i][j] += triangle[i - 1][j-1];//끝값을 더해준다
			}
			else//처음 인덱스값과 끝 인덱스 사이의 값들을 비교해서 더해준다
			{
				triangle[i][j] += max(triangle[i - 1][j - 1] , triangle[i - 1][j]);
			}
		}
		if (i == triangle.size() - 1)
			answer = *max_element(triangle[i].begin(), triangle[i].end());
	}
	

	return answer;
}
```

___

문제설명:

1. 삼각형의 꼭지점은 고정이므로 삼각형의 두번째줄부터 비교를 합니다.
2. 삼각형의 행에서 시작과 끝은 각각 왼쪽과 오른쪽으로만 덧셈을 진행하고 가운데 있는 숫자에서는 그 이전행의 전값들 중에 큰값하고만 더해서 자신의 자리에 그 더해진 값으로 채워넣습니다.
3. 위의 과정을 반복 시행한 후 최종 행까지 계산이 끝나면 그 행에서 가장 큰 원소를 반환합니다.





사용언어:c++

출처: https://programmers.co.kr/learn/courses/30/lessons/43105