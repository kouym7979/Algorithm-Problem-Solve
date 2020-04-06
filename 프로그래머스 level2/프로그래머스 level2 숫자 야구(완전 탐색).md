## 프로그래머스 level2 숫자 야구(완전 탐색)

###### 문제 설명

숫자 야구 게임이란 2명이 서로가 생각한 숫자를 맞추는 게임입니다. 

각자 서로 다른 1~9까지 3자리 임의의 숫자를 정한 뒤 서로에게 3자리의 숫자를 불러서 결과를 확인합니다. 그리고 그 결과를 토대로 상대가 정한 숫자를 예상한 뒤 맞힙니다.

```
* 숫자는 맞지만, 위치가 틀렸을 때는 볼
* 숫자와 위치가 모두 맞을 때는 스트라이크
* 숫자와 위치가 모두 틀렸을 때는 아웃
```

예를 들어, 아래의 경우가 있으면

```
A : 123
B : 1스트라이크 1볼.
A : 356
B : 1스트라이크 0볼.
A : 327
B : 2스트라이크 0볼.
A : 489
B : 0스트라이크 1볼.
```

이때 가능한 답은 324와 328 두 가지입니다.

질문한 세 자리의 수, 스트라이크의 수, 볼의 수를 담은 2차원 배열 baseball이 매개변수로 주어질 때, 가능한 답의 개수를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 질문의 수는 1 이상 100 이하의 자연수입니다.
- baseball의 각 행은 [세 자리의 수, 스트라이크의 수, 볼의 수] 를 담고 있습니다.

##### 입출력 예

| baseball                                             | return |
| ---------------------------------------------------- | ------ |
| [[123, 1, 1], [356, 1, 0], [327, 2, 0], [489, 0, 1]] | 2      |

##### 입출력 예 설명

문제에 나온 예와 같습니다.

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
using namespace std;

//숫자는 맞지만 위치가 틀렸을 때 볼
//숫자와 위치가 모두 맞으면 스트라이크
//숫자와 위치가 모두 틀렸을 때는 아웃
//세자리수, 스트라이크의 수 , 볼의 수
//123~987까지 탐색 서로 다른 자릿 수

int solution(vector<vector<int>> baseball) {
	int answer = 0;//가능한 답의 개수
	
	string base = "";//가능한 답을 저장 
	string temp = "";
	int check = true;
	for (int i = 123; i <= 987; i++)
	{
		base = to_string(i);
		if (base[0] == base[1] || base[0] == base[2] || base[1] == base[2])//각 자리수가 달라야 하므로
			continue;
		else if (base[0] == '0' || base[1] == '0' || base[2] == '0')
			continue;
		check = true;
		for (int t = 0; t < baseball.size(); t++)
		{
			int strike = 0;
			int ball = 0;
			for (int j = 0; j < 3; j++)
			{
				for (int a = 0; a < 3; a++)
				{
					temp = to_string(baseball[t][0]);//입력받은 수와 비교
					if (j == a && base[j] == temp[a]) {//자리가 같고 숫자가 같은 경우
						strike++;
						continue;
					}
					if (j != a && base[j] == temp[a])//자리가 다르지만 숫자가 같은경우
					{
						ball++;
						continue;
					}
				}
			}
			if (baseball[t][1] != strike || baseball[t][2] != ball)//조건과 다르면 false
			{
				check = false;
				break;
			}
		}
		if (check == true)
			answer++;
		
	}


	return answer;

}
```

문제 해설: 조건에서 각 자리의 수는 다른 999이하의 수이므로 전체의 경우는 123~987까지의 수를 탐색해서 조건에 부합하는 숫자들의 개수를 출력하는 문제입니다.

1. 123~987까지의 수를 문자열로 base에 넣어둡니다. 이때 각 자리의 수가 서로 달라야하며 각 자리수에 0이들어가는 경우는 continue로 포문 자체를 넘겨서 진행시킵니다.
2. 이제 입력받은 수를 temp에 문자열에 넣고 base와 temp의 각 자리를 비교해서 strike와 ball의 수를 설정합니다.
3. strike의 수와 ball의 수가 입력된 수와 다를 경우 break를 하고 다시 위의 과정을 반복하고 같을경우에는 answer의 수를 증가시키고 위의 과정을 반복합니다.



이번 문제는 123~987까지의 수들의 경우만 확인하면 되어서 완전탐색으로 풀어보았습니다. 만약 경우의 수가 더 많았다면 완전탐색으로 하기에는 효율이 안좋을 수 있다는 생각이 들어서 다른 방법도 생각해보도록 하겠습니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42841